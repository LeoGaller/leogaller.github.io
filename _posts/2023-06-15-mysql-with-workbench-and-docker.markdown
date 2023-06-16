---
layout: post
title:  "MySQL with workbench using Docker"
date:   2023-06-15 22:00:00 -0300
categories: Spark
author:
- Leonardo Galler
meta: "MySQL"
---
<div style="text-align: justify" markdown="1">

![MySQL](https://www.mysql.com/common/logos/logo-mysql-170x115.png "Lightweight and Powerful!")

Sometimes in your efforts to learn new technologies, you have the necessity to test new tools and learn new abilities, like the use of databases and SQL.

# Starting well
With this post, I would like to give anyone a way to quickly start developing and using MySQL and Workbench in their studies.

## Tools
1. **MySQL:**<br>
![MySQL Inside](https://www.mysql.com/common/logos/powered-by-mysql-125x64.png "Lightweight database")<br>
> MySQL is the world's most popular open source database. With its proven performance, reliability and ease-of-use, MySQL has become the leading database choice for web-based applications, covering the entire range from personal projects and websites, via e-commerce and information services, all the way to high profile web properties including Facebook, Twitter, YouTube, Yahoo! and many more.<br>
Source: [MySQL Official Page](https://www.mysql.com/)

2. **MySQL Workbench:**<br>
![MySQL Workbench](https://www.mysql.com/common/images/products/MySQL_Workbench_Mainscreen_Windows.gif "Data Tool")<br>
> MySQL Workbench is a unified visual tool for database architects, developers, and DBAs. MySQL Workbench provides data modeling, SQL development, and comprehensive administration tools for server configuration, user administration, backup, and much more. MySQL Workbench is available on Windows, Linux and Mac OS X.<br>
Source: [MySQL Workbench Official Page](https://www.mysql.com/products/workbench/)

3. **Docker:**<br>
![Docker](https://www.docker.com/wp-content/uploads/2022/03/horizontal-logo-monochromatic-white.png "Docker")<br>
> Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.<br>
Source: [Docker Official Page](https://docs.docker.com/get-started/overview/)

## Identifying the problem
**_I need a database and a tool for data modeling and querying using SQL!_**<br>
To fast start your studies or analysis on any of these tools you should be able to have it in minutes and not hours or even worse manipulating huge VM images.

### Step-by-step
1. Install docker and check if it working.
  * On [windows](https://docs.docker.com/desktop/install/windows-install/)
  * On [Mac](https://docs.docker.com/desktop/install/mac-install/); For Mac you will have the option of chip, verify what is yours before.
  * On [Linux](https://docs.docker.com/desktop/install/linux-install/)

2. Open the terminal
3. Pull the docker image for [MySQL](https://hub.docker.com/_/mysql/)<br>
~~~ shell
docker pull mysql 
~~~
![docker pull](({{site.url}}/images/docker-pull.png "Ran Successfully"))

## Conclusion

When developing new applications always remember of:
1. Scalability: Plan to different sizes of data volume;
2. Reliability: Make tests to asure the solution you developed can handle many situations;
3. Performance: Assess the time and consumption of resources to the best distribution of cluster resources;
4. Maintainability: Keep it simple so it can be replicated and reused.

And with those basics ideas and solutions that I shared, your Spark applications will run satisfactorily.

</div>