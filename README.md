# Snowpark Connect Using Jupyter

Run the same PySpark code on either local Apache Spark or Snowflake via Snowpark Connect. This repo contains the notebook `snowpark-connect-jupyter-blog.ipynb` demonstrating a full pipeline: data generation, cleaning/feature engineering, UDFs, and SQL analytics. Switching engines is a single flag change.

## Prerequisites
- Conda (Anaconda/Miniconda)
- Python 3.12
- Jupyter
- For Snowpark Connect: Snowflake account and Snowflake CLI configured

## Environment setup

Snowpark Connect
```bash
conda create -n snowpark-connect-demo python=3.11
conda activate snowpark-connect-demo
conda install -c conda-forge pyspark matplotlib seaborn jupyter
pip install snowpark-connect
```

Snowflake CLI (required for Snowpark Connect)
```bash
pip install snowflake-cli-labs
snow connection add --connection-name spark-connect \
  --account your-account \
  --user your-username \
  --password \
  --database your-database \
  --schema your-schema \
  --warehouse your-warehouse
```

## Run the notebook
1. Open `snowpark-connect-jupyter-blog.ipynb` in Jupyter/Lab.
2. In the configuration cell, set:
   - `CONDA_ENV_NAME = "your-env"`
   - `USE_SNOWPARK_CONNECT = True` for Snowflake, or `False` for local Spark
3. Run cells top-to-bottom.

## What it does
- Generates 50k NYC taxi trips
- Cleans and enriches data (hour/day, duration, speed)
- Applies UDFs (trip category, tip percentage)
- Runs SQL analytics (trip stats, peak hours, payment analysis)
- Prints an execution summary to validate identical behavior across engines

## Switching engines
- Snowpark Connect: session via `snowpark_connect.get_session()`
- Local Spark: session via `SparkSession.builder.getOrCreate()`

All downstream code is identical.

## Resources
- Snowpark Connect docs: https://docs.snowflake.com/en/developer-guide/snowpark-connect/snowpark-connect-overview
- Snowflake CLI setup: https://docs.snowflake.com/en/developer-guide/snowflake-cli/connecting/specify-credentials
- PySpark install: https://spark.apache.org/docs/latest/api/python/getting_started/install.html

