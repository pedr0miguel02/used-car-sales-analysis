# Used Car Auction Sales Analysis: United States (2014–2015)

An exploratory analysis of 553,000 used car sales at US auctions, done in Python in a single Jupyter notebook. The project follows the usual data analysis workflow: loading, quality checks, cleaning, exploratory analysis, visualization and conclusions.

## Questions

1. Does the selling price follow the reference market value? When does it move away from it?
2. How much value does a car lose with age and mileage?
3. Which body types and makes sell the most, and at what price?
4. Which states have the most sales?

## Data

- **File:** `car_prices.csv` (558,837 rows, 16 columns), published on Kaggle as [*Vehicle Sales Data*](https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data).
- **Contents:** one row per car sold, with make, model, year, body type, transmission, condition, odometer, US state, sale date, selling price and market value (MMR, *Manheim Market Report*).
- **Period:** December 2014 to July 2015.
- **Map:** `us_states.geojson`, with US state boundaries from [Natural Earth](https://www.naturalearthdata.com/) (public domain).
- I could not find a license or an official data dictionary for the dataset.

## Cleaning

- Removed **26 misaligned rows**, where values had shifted one column to the right.
- Removed **7 impossible prices**: cars sold for $1, or with an extra digit.
- Removed **sales in Canada** (1%), because prices may have been in a different currency.
- Put **condition on a single 1–5 scale**. The file mixed values from 1 to 5 with values from 11 to 49. The scale is inferred from the data: the values 10, 20, 30, 40 and 50 never appear, and prices match.
- **Standardized** makes (for example, "ford tk" becomes "ford") and grouped 87 body names into 9 types.
- Treated **odometer = 999,999** as a missing value.
- Kept **repeated VINs**, because they are resales of the same car on different dates.
- Did **not fill in** any missing values.

## Charts

Nine charts of different types, each linked to one question:
- line chart: depreciation by age;
- violin plot: price distribution by age band;
- bar chart: best-selling makes;
- two box plots: price by body type, and difference from market value by condition;
- scatter plot: market value vs. selling price;
- correlation heatmap;
- pair plot;
- map of the US with sales by state.

## Key findings

- Selling price follows market value (correlation of **0.98**, median difference of −0.4%). The exception is cars in poor condition: grade 1 cars sell **19.3% below** market value.
- A car loses about **80% of its value in 10 years**, for sedans, SUVs and pickups alike.
- **Ford, Chevrolet and Nissan** account for 37.5% of sales. Luxury brands have a median price about twice that of mainstream brands.
- **Florida, California and Pennsylvania** together account for 38.0% of sales.

These are associations, not cause and effect: older cars also have more miles and worse condition.

## Limitations

The period is short and some months have almost no data, so there is no trend analysis. There are no costs, so there is no profit analysis. The condition scale is inferred from the data, and the state is where the auction took place, not where the buyer lives. Section 8 of the notebook covers these limitations in more detail.

## Tools

Python, pandas, Matplotlib, seaborn, geopandas and Jupyter Notebook.

## How to reproduce

1. Download `car_prices.csv` from Kaggle (link above) and put it in the same folder as `used_car_sales_analysis.ipynb` and `us_states.geojson`.
2. Install the libraries:
   ```bash
   pip install pandas matplotlib seaborn geopandas jupyter
   ```
3. Open the notebook and run all cells in order:
   ```bash
   jupyter notebook used_car_sales_analysis.ipynb
   ```

The notebook was tested end to end with pandas 3.0 / seaborn 0.13 / geopandas 1.2 and with pandas 2.2 / seaborn 0.12 / geopandas 0.14. With seaborn 0.12, the library shows internal warnings (`FutureWarning`) in the violin plot and the pair plot; they do not affect the results. They do not appear with seaborn 0.13 or later.

## Project structure

```
├── used_car_sales_analysis.ipynb   # full analysis
├── us_states.geojson               # US state boundaries (for the map)
├── car_prices.csv                  # original data (not included in the repository: 88 MB)
└── README.md
```
