---
layout: post
title:  "Spark Tuning for Data skewing and low parallelism."
date:   2022-09-01 21:38:31 -0300
categories: Spark
author:
- Leonardo Galler
meta: "Spark"
---
<div style="text-align: justify" markdown="1">

![Apache Spark](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Apache_Spark_logo.svg/128px-Apache_Spark_logo.svg.png "The main tool for data engineering!")

Apache spark is the de facto tool for data engineering, you can confirm that just looking at the companies that trust Spark to handle their data engineering efforts.

# But...
By the quantity of languages and types of applications spark can handle you can expect some difficulties to arise. And the main issues are related to <b>Data Skew</b> and <b>Low Parallelism</b>, and these are the issues we will focus now.

## Defining the problems
1. **Data Skew**: <br>
  ![Data Skew]({{site.url}}/images/data-skew.png "The statistical definition")<br>
In Statistical terms a data skewing is refered to the value distribution that is or become uneven, as can be seen in the first image.
Data skewing in computational systems for data processing normally is caused by transformations applied to the data. Some of these trasnformations are *Join, groupBy* and *orderBy*.<br><br>
    ![Data Skew in Spark]({{site.url}}/images/skew-park.png "Visual reference of skewness of data in Sparks")<br>
This situation often happens when you are trying to join tables that are not well distributed in the nodes of the cluster, this can make some partitions to become much higher than the others causing spark not to properly process the data in parallel.

2. **Low Parallelism:**
The spark processing will not fully use the cluster resources until the level of parallelism for each operation is high enough. For this reason, the main source of low level of parallelism is data skewing. We know that data skewing is directly connected to partitions and it cause low parallelism.<br><br>
![Data Skew in Spark]({{site.url}}/images/low-parallelism.png "Just 2 tasks processing 128 partitions")<br>
In the above example we can see that only 2 executors are processing 128 partitions even though there are 12 executors available but were not used to process the data.
Low paralelism makes the time of the longer running stage be the bottleneck of the whole processing.

## Identifying the problem
**How to know if I have data skewness?**<br>
You can get evidences from:
1. Running counts against the partitions of the dataframe;
2. Verifying the Web UI of the SparkContext of your application and look for task and stages that are taking longer than the others to finish.

### Running counts against the partitions of the dataframe
After you read the data to a dataframe called 'df' you can call the function [spark_partition_id](https://spark.apache.org/docs/3.1.1/api/python/reference/api/pyspark.sql.functions.spark_partition_id.html). This function when called determines the key(s) of the partitions in a dataframe. 
Find below an example command to find the number of partitions and plot it using jupyter notebooks:</div>
```
%python
df_partition_counts = df.groupBy(spark_partition_id()) \
    .count() \
    .orderBy(desc("count"))
```
<div style="text-align: justify" markdown="1">
You can see below an example output:<br>

![Counting the rows per partition]({{site.url}}/images/partition-count.png "Data skew in a spark dataframe")<br>

### Verifying the Web UI and analyzing the size of data processed by stage/task or the time taken.
Other way to perform this analysis without the need to write and execute code is to look at the [web UI](https://spark.apache.org/docs/latest/web-ui.html) of the application and analyze the tasks.
After accessing the web UI you go to the Stages Tab.
Stages for all jobs:

![All Stages Detail]({{site.url}}/images/AllStagesPageDetail3.png)

In the example below you can see that the first task is processing almost all the data alone, and does this at the risk of crashing the node of the cluster and taking all of the processing time.

![One task holding all the job time]({{site.url}}/images/bad-data-skew.png)

</div>