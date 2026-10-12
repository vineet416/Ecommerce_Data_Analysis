# E-commerce Data Analysis (Python + MySQL)

Loads a seven-table Brazilian e-commerce dataset into MySQL with Python, then answers 15 business questions in SQL.
Results are pulled into pandas and charted with Matplotlib/Seaborn. It covers customers, orders, categories, sellers and sales trends.

## Project Files

| File | Description | 
|---|---|
| `Ecommerce_csv_to_sql.ipynb` / `.pdf` | Loads the 7 CSVs into MySQL tables (dynamic `CREATE TABLE` + row inserts) |
| `python+sql_ecommerce.ipynb` / `.pdf` | 15 SQL queries run from Python, with outputs and charts |
| `Questions.txt` | The 15 questions (5 basic, 5 intermediate, 5 advanced) |
| `dataset_link.txt` | Kaggle link to the source dataset |

## Dataset

Source: Kaggle (`dataset_link.txt`). CSVs are not stored in this repo.

| Table | Columns |
|---|---|
| `customers` | customer_id, customer_unique_id, zip_code_prefix, city, state |
| `orders` | order_id, customer_id, order_status, purchase / approved / carrier / delivered / estimated-delivery timestamps |
| `order_items` | order_id, order_item_id, product_id, seller_id, shipping_limit_date, price, freight_value |
| `payments` | order_id, payment_sequential, payment_type, payment_installments, payment_value |
| `products` | product_id, product category, name/description length, photos_qty, weight_g, length/height/width_cm |
| `sellers` | seller_id, zip_code_prefix, city, state |
| `geolocation` | zip_code_prefix, lat, lng, city, state (loaded, never queried) |

## Approach

1. **Understand the data:** read each CSV with pandas and count NaNs per column.
2. **Clean and load:** swap NaN for `NULL`, tidy column names, map dtypes to SQL types, insert row by row.
3. **Analyse:** run basic, intermediate and advanced SQL (joins, CTEs, window functions, `LAG`, `DENSE_RANK`).
4. **Report:** show results as DataFrames and bar/line/scatter charts; export notebooks to PDF.

## Key Insights

Tags: ✅ recomputed from the data, 📓 taken from the notebook output (raw tables not available to re-run).

| Finding | Number | Source |
|---|---|---|
| Customers are concentrated in São Paulo state | SP 41,746 of 99,441 (42.0%); top 3 states (SP, RJ, MG) = 66.6% | ✅ |
| One city dominates | `sao paulo` 15,540 customers (15.6%); 4,119 cities, 27 states | ✅ |
| Repeat buyers are rare | 2,997 of 96,096 unique customers (3.1%) have more than one `customer_id` | ✅ |
| Orders in 2017 | 45,101 | 📓 |
| 2018 order peak | Jan 7,269, Mar 7,211; June is the low among full months (6,167) | 📓 |
| Top categories by sales (price + freight) | Health beauty ≈1,441k, watches ≈1,306k, bed/table/bath ≈1,242k | 📓 |
| Top categories by revenue share | Bed/table/bath 10.70%, health beauty 10.35%, computer accessories 9.90% | 📓 |
| Sales growth | 2018 vs 2017: +20.0% (2018 covers about 8 months); cumulative sales ≈16M by Aug 2018 | 📓 |
| Price vs. volume | Correlation −0.11 across categories (weak) | 📓 |
| Seller concentration | Top seller 507,167 vs #2 at 308,222 (1.6×) | 📓 |

## Tech Stack

- **Language:** Python in Jupyter Notebook
- **Libraries:** pandas, NumPy, Matplotlib, Seaborn, mysql-connector-python
- **Database:** MySQL (database `ecommerce`)
- **Techniques:** ETL, joins, CTEs, window functions, aggregation, data visualisation

## How to Use

1. Download the CSVs from the link in `dataset_link.txt` and place them in one folder.
2. Install dependencies: `pip install pandas numpy matplotlib seaborn mysql-connector-python`
3. Create the database: `CREATE DATABASE ecommerce;`
4. In both notebooks, set your MySQL credentials; in the loader notebook, also set `folder_path` (hard-coded to `E:/Ecommerce`).
5. Run `Ecommerce_csv_to_sql.ipynb` to load the tables, then `python+sql_ecommerce.ipynb` for the analysis.
6. Or just read the `.pdf` exports to see the results without running anything.
