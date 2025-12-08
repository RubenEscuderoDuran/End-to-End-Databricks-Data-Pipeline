# End-to-End-Databricks-Data-Pipeline

I designed and built an end-to-end data pipeline in Databricks using the Medallion architecture (Bronze–Silver–Gold) for a sales use case (orders, customers, products, regions), focusing on incremental ingestion, dimensional modeling and analytics.

The solution includes: Auto Loader ingestion from ADLS into Bronze, a unified Silver notebook for cleansing and enrichment, a DimCustomers table with a surrogate key and SCD Type 1 logic implemented via Delta MERGE (with an init_load_flag to control full vs incremental loads), a DimProducts table built from Silver, and a FactOrders table linking orders to both dimensions with foreign keys. Finally, I created an analysis notebook with SQL queries for daily/monthly sales, top customers/products, sales by domain, category and brand, and price-band / discount scenarios.

Technologies: Databricks, PySpark, SQL, Delta Lake, Auto Loader, Unity Catalog, dimensional modeling (star schema), incremental loads with MERGE.