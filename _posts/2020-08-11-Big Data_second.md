---
title: "Big Data - part2"
date: 2020-08-11 09:30:00
categories: programming
---
### Pyspark Dataframe basic operation
```python
# Install Java, Spark, and Findspark
!apt-get update
!apt-get install openjdk-8-jdk-headless -qq > /dev/null
!wget -q http://www-us.apache.org/dist/spark/spark-2.4.6/spark-2.4.6-bin-hadoop2.7.tgz
!tar xf spark-2.4.6-bin-hadoop2.7.tgz
!pip install -q findspark
# Set Environment Variables
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64"
os.environ["SPARK_HOME"] = "/content/spark-2.4.6-bin-hadoop2.7"
# Start a SparkSession
import findspark
findspark.init()
```
```python
# Start Spark Session
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("DataFrameBasics").getOrCreate()
```
### Construct DataFrame-1 Manually construct
```python
df = spark.createDataFrame([(index_1, value1), (index_2, value2), (index_3, value3),...], ["id", "words"] )
df.show()
```
### Construct DataFrame-2 Read in data from S3 Buckets
```python
from pyspark import SparkFiles
url = "https://s3.amazonaws.com/dataviz-curriculum/day_1/food.csv"
spark.sparkContext.addFile(url)
df = spark.read.csv(SparkFiles.get("food.csv"),sep=",", header=True)
```
### Construct DataFrame-3 Read in data with struct field for schema
```python
from pyspark import SparkFiles
url = "https://s3.amazonaws.com/dataviz-curriculum/day_1/food.csv"
spark.sparkContext.addFile(url)
from pyspark.sql.types import StructField, StringType, IntegerType, StructType
schema = [StructField("food",StringType(),True), StructField("price",IntegerType(), True),]
final = StructType(fields=schema)
df = spark.read.csv(SparkFiles.get("food.csv"),schema=final, sep=",", header=True)
```

### Basic Operation
```python
# Accessing Data
dataframe['price'] //columns opject
dataframe.select('price') // dataframe
dataframe.select('price').show()

# Manipulating Columns
dataframe.withColumn('newprice', dataframe['price']*2 ) //add new column. it should be assigned to a new dataframe
dataframe.withColumnRenamed('price','newprice') // update column name

# Statistics summary
dataframe.describe().show()
dataframe.select([...]).describe().show()

# Collecting a column as a list
dataframe.select('price').collect()

# converting to a panda dataframe
import pandas as pd
pandas_df = dataframe.toPandas()
pandas_df.head()
```
### Filtering, Ordering
```python
# ordering
df.orderBy(df["points"].asc()).show(5)
df.orderBy(df["points"].desc()).show(5)
df.orderBy("points").select("occupations").show()

# import average funtion
from pyspark.sql.functions import avg, min, max
df.select(avg("points")).show()
df.select(min("points")).show()
df.select(max("points")).show()

# using filter
df.filter("price<20").show()
df.filter("price<20").select(["points","country","winery","price"]).show()
#using filter with python comparison operators
df.filter(df["price"] < 200).show()
df.filter((df["price"]<200) | (df["points"]>80)).show()
df.filter(df["country"]=="US").show()

# using groupby
df.groupBy("academic_degree").avg() // groupby + average
df.groupBy("academic_degree").agg(avg("age")).show()
df.groupBy("academic_degree","occupation").count().show()
```
### Date
```python
from pyspark import SparkFiles
url ="https://s3.amazonaws.com/dataviz-curriculum/day_1/rainfall.csv"
spark.sparkContext.addFile(url)
df = spark.read.csv(SparkFiles.get("rainfall.csv"), sep=",", header=True, inferSchema=True, timestampFormat="yyyy/MM/dd HH:mm:ss")
df.show()
```
```python
from pyspark.sql.functions import year, month
df.select(year(df["date"])).show()
df=df.withColumn("year", year(df["date"]))
averages = df.groupby("year").avg()
averages.orderBy("year").select("year","avg(prcp)").show()
```
