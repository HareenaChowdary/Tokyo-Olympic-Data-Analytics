# Tokyo-Olympic-Data-Analytics

## 📌 Project Overview
This project demonstrates an end-to-end Azure Data Engineering pipeline for analyzing Tokyo Olympic data. It leverages Azure services such as Azure Data Factory, Databricks, Azure Data Lake, Azure Synapse Analytics, and visualization tools like Power BI, Looker Studio, and Tableau.

### 🔹 Key Components
1. **Data Source**: Tokyo Olympic dataset.
2. **Data Ingestion**: Data is ingested using Azure Data Factory.
3. **Storage**: Raw data is stored in Azure Data Lake Gen2.
4. **Transformation**: Databricks and PySpark are used to process and clean the data.
5. **Analytics**: Transformed data is stored in Azure Synapse Analytics for querying.
6. **Visualization**: Dashboards are created using Power BI, Looker Studio, and Tableau.

---

## 🛠️ Technologies Used
- **Azure Data Factory** (Data ingestion)
- **Azure Data Lake Gen2** (Storage)
- **Azure Databricks** (Data processing & transformation using PySpark)
- **Azure Synapse Analytics** (Data warehousing)
- **Power BI, Looker Studio, Tableau** (Data visualization)

---

## 🔧 Data Processing in Databricks
Below is an overview of the data processing steps performed using PySpark:

```python
from pyspark.sql.functions import col
from pyspark.sql.types import IntegerType

# Mount Azure Data Lake Storage
configs = {"fs.azure.account.auth.type": "OAuth", ...}
dbutils.fs.mount(source="abfss://tokyo-olympic-data@tokyoolympicdatadlsg.dfs.core.windows.net", mount_point="/mnt/tokyoolympic", extra_configs=configs)

# Read data
athletes = spark.read.format("csv").option("header","true").load("/mnt/tokyoolympic/raw-data/athletes.csv")
medals = spark.read.format("csv").option("header","true").load("/mnt/tokyoolympic/raw-data/medals.csv")

# Data transformation
medals = medals.withColumn("Gold", col("Gold").cast(IntegerType()))

# Write transformed data
athletes.write.mode("overwrite").option("header",'true').csv("/mnt/tokyoolympic/transformed-data/athletes")
```

---

## 📊 Insights Generated
- **Top countries with the highest number of gold medals**
- **Average number of entries by gender for each discipline**
- **Distribution of athletes and coaches by country**

---

## 🚀 How to Run the Project
1. **Setup Azure Resources**: Create an Azure Data Factory, Data Lake, and Databricks workspace.
2. **Upload Data**: Store raw data in Azure Data Lake Gen2.
3. **Run Databricks Notebook**: Execute PySpark code to process data.
4. **Load Data into Synapse**: Use Azure Synapse for querying and analytics.
5. **Create Dashboards**: Use Power BI, Looker Studio, or Tableau for visualization.

---


