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

### Defining the problem
1. Data Skew: ![Data Skew](../_images/data-skew.png)
In Statistical terms a data skewing is refered to the value distribution
2. Low Parallelism: 