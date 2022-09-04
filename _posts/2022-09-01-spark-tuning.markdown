---
layout: post
title:  "Spark Tuning for Data skewing and low parallelism."
date:   2022-09-01 21:38:31 -0300
categories: Spark
author:
- Leonardo Galler
meta: "Spark"
---
![Apache Spark](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Apache_Spark_logo.svg/128px-Apache_Spark_logo.svg.png "The main tool for data engineering!")

Apache spark is the de facto tool for data engineering, you can confirm that just looking at the companies that trust Spark to handle their data engineering efforts.

## But...
By the quantity of languages and types of applications spark can handle you can expect some difficulties to arise. And the main issues are related to <b>Data Skew</b> and <b>Low Parallelism</b>, and these are the issues we will focus now.

## Defining the problem
1. Data Skew: 
   
    ![Data Skew](_site/images/data-skew.png "The statistical definition")<br>
In Statistical terms a data skewing is refered to the value distribution that is or become uneven, as can be seen in the first iamge.
Data skewing in computational systems for data processing normally is caused by transformations applied to the data. Some of these trasnformations are *Join, groupBy* and *orderBy*.<br><br>
    ![Data Skew in Spark](_site/images/skew-park.png "Visual reference of skewness of data in Sparks")<br>
This situation often happens when you are trying to join tables that are not well distributed in the nodes of the cluster, this can make some partitions to become much higher than the others causing spark not to properly process the data in parallel.

1. Low Parallelism: 