# End-to-End-Databricks-Data-Pipeline
I design end-to-end Databricks data pipeline and built using the Medallion architecture (Bronze → Silver → Gold) for a synthetic sales dataset (orders, customers, products, regions).

- Implemented incremental ingestion from Azure Data Lake with Auto Loader into Bronze for orders, customers and products.

- Built a unified Silver notebook to clean data, fix types and enrich features (e.g. full_name, email domain, price_band, discount_price).

- Designed DimCustomers with a surrogate key (DimCustomerKey), create_date / update_date tracking and SCD Type 1 logic using Delta MERGE, controlled by an init_load_flag parameter for full vs incremental loads.

- Created Gold tables for DimProducts (using a Lakeflow/Delta Live Tables pipeline) and FactOrders, modeling a proper star schema ready for analytics.

- Added an Analysis notebook with SQL queries for daily/monthly sales, top customers/products, sales by category/brand and price-band scenarios.

# Gold Products
Delta Live Tables / Lakeflow pipeline that builds dimproducts in Gold. It stages product data, applies transformations in dimproducts_view, and writes a streaming DimProducts table with 500 products fully processed.
![](https://github.com/RubenEscuderoDuran/End-to-End-Databricks-Data-Pipeline/blob/main/DLT.png)


# End_to_Pipeline Job
Databricks Job that orchestrates the full Medallion flow: Parameters → Bronze_Autoloader_iteration → Silver → Gold_Customers → Gold_Products → Gold_Orders → Analysis. The run finished successfully, proving the entire pipeline can be executed end-to-end in about 12 minutes on a single-node cluster.
![](https://github.com/RubenEscuderoDuran/End-to-End-Databricks-Data-Pipeline/blob/main/End-Pipeline.png)

