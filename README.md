# Sephora Products Analysis: what drives ratings and pricing

Data-quality audit and business analysis of Sephora's product catalogue (about 8.5K products, 27 fields) using **Python, SQL (SQLite) and Power BI**.

**Business question:** how do price, brand and category relate to customer ratings and review volume, and where should a brand or category manager look first?

## What is in this repo

| Path | Content |
|---|---|
| `notebooks/sephora_analysis.ipynb` | Full workflow: load, audit, clean, SQL analysis, charts, export |
| `sql/queries.sql` | The 10 SQL queries used (category, brand, price band, exclusives, sale status, window-function ranking, high-volume low-rated products) |
| `docs/powerbi_dashboard_spec.md` | Layout, KPIs and DAX measures for the 3-page Power BI dashboard |
| `images/` | Charts exported by the notebook |
| `data/processed/` | Cleaned dataset and summary tables created by the notebook (Power BI input) |
| `data/raw/` | Put `product_info.csv` here (not committed, see below) |

## How to run

1. Download `product_info.csv` from the [Kaggle dataset](https://www.kaggle.com/datasets/nadyinky/sephora-products-and-skincare-reviews) and save it as `data/raw/product_info.csv`.
2. `pip install -r requirements.txt`
3. Open `notebooks/sephora_analysis.ipynb` and run all cells. Charts land in `images/`, tables in `data/processed/`.

## Method

1. **Audit:** missing values per field, duplicate product IDs, products without rating or review count, price outliers (IQR rule).
2. **Clean, with every decision documented in the notebook:** no zero-filling of missing ratings, no deletion of outliers (flagged instead), sparse sale/value price fields kept only as an `is_on_sale` flag.
3. **SQL:** aggregate comparisons by category, brand, price band and product flags; a window function ranks the top products per category; a query isolates high-review-volume products rated below the catalogue average.
4. **Visualise and report:** four charts and a Power BI dashboard.

## Results

> Fill this section after running the notebook, using the numbers printed in section 5 and the `CV NUMBERS` line at the end. Do not copy figures from anywhere else.

- Data quality: `<N>` products with no rating or review count (`<x>%`); `<N>` price outliers; sale and value price fields `<x>%` empty.
- Finding 1: `<category with the highest review volume and its rating gap>`
- Finding 2: `<price band vs rating result>`
- Recommendation: `<one concrete action for a brand or category manager>`

## Limitations

- Ratings are self-selected customer reviews, so they skew positive and show association, not causation.
- The data is a single snapshot, so trends over time cannot be analysed.
- Skincare-focused source data may not represent Sephora's full range.

## Author

Chhavi Jain, MSc Data Analytics for Business, Kedge Business School. [LinkedIn](https://www.linkedin.com/in/chhavijainkedgebs)
