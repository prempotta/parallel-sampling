# Parallel Sampling

## Introduction ##

This notebook demonstrates a framework for parallel sampling from large amounts of data by leveraging spark.

## Setup ##

1.  Import the Notebook "ParallelSampling.ipynb" into Databricks
2.  Download the sample data from [here](https://drive.google.com/drive/folders/1-zU8q1Jgif4p4RfwOcX6PlKFY9WadgG-)
3.  Upload the files of the sample data into databricks, and change the paths of the files in the configuration part of the notebook accordingly.
4.  Verify whether all the cells in the notebook are able to be executed by selecting "Run All" option in the notebook.

## Running the notebook for a different set of data ##

You mainly need to create three files: 

1.  Input Schema
2.  Input Data JSON
3.  Output Schema

### Input Schema ###

1.  Make a copy of "orders_data_schema.avsc" file.
2.  Modify the Avro schema accordingly for your usecase. 
3.  Mainly, you need to change the change the fields under the section "data" according to your new data. You can refer this [link](https://avro.apache.org/docs/1.11.1/specification/) to learn more about how to create an Avro schema.
4.  Upload the newly created .avsc file to databricks, and change the path in the "INPUT_SCHEMA_PATH" configuration parameter of the notebook.

### Input Data JSON ###

1.  Make a copy of "orders_data.json" file.
2.  Replace the contents of the "data" section with your own data as an array of records.
3.  Change the sampling parameters according to your usecase:
	1.  "filter" contains the Spark SQL SELECT query to filter the data according to your requirements. 
	    *  An example of a filter could be: "SELECT * FROM data WHERE ZONE_ID>2000". This query filters the orders containing zone id greater than 2000 from the entire dataset of orders. You need to perform the SELECT query from a table called "data" as shown in the example. 
	    *  You can refer to this [link](https://spark.apache.org/docs/latest/sql-ref-syntax-qry-select.html) to understand how to write SELECT queries in Spark SQL.
	 2.  "samplingRate" defines the fraction of the filtered data that you want to sample. Enter a value between 0 to 1. For example, 0.1 indicates that we want to sample 10% of the filtered data.
	 3. "samplingType" defines the type of sampling you want to perform. For now, we only support "random" sampling.
4.  Upload the newly created .json file to databricks, and change the path in the "DATA_PATH" configuration part of the notebook.

### Output Schema ###

1.  Make a copy of "output_schema.avsc" file.
2.  Modify the Avro schema accordingly for your usecase. 
3.  Mainly, you need to change the change the fields according to your new data. You can refer to this [link](https://avro.apache.org/docs/1.11.1/specification/) to learn more about how to create an Avro schema.
4.  Upload the newly created .avsc file to databricks, and change the path in the "OUTPUT_SCHEMA_PATH" configuration part of the notebook.
