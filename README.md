# 1. Glue Job: Bronze to Silver Data Lake ETL

## Description

This AWS Glue job reads raw data files from S3 (bronze layer), applies basic transformations, and writes the processed data into Hudi tables (silver layer) registered in the Glue Catalog.

### Steps

1. **Read Input Data**  
   Reads three input files from S3 and creates a DataFrame for each:
   - customers
   - products
   - transactions

2. **Transform Data**  
   Applies basic string transformations and adds a `load_date` column to each DataFrame.

3. **Write to Hudi Tables**  
   Writes each DataFrame to a Hudi table in S3 and registers the tables in the Glue Catalog.

## Parameters

- `--conf spark.serializer=org.apache.spark.serializer.KryoSerializer`
- `--conf spark.sql.hive.convertMetastoreParquet=false`
- `--datalake-formats hudi`
- `--bucket_name <your_bucket_name>`
- `--ip_path <input_raw_files_path>`
- `--op_path <output_silver_files_path>`

## Notes

- Hardcoded values for database and table names are used in the code.  
  You can modify these as needed.
- The job uses Hudi for upsert operations and partitioning by `load_date`.

## Usage

1. Update the parameters with your S3 bucket and paths.
2. Run the Glue job using the provided script
3. The processed data will be available in the specified output path as Hudi tables.
