---
layout: post
title:  "MySQL with workbench using Docker"
date:   2023-06-15 22:00:00 -0300
categories: Docker
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
  * On [Linux](https://docs.docker.com/desktop/install/linux-install/)<br><br>

2. Open the terminal<br><br>
3. Pull the docker image for [MySQL](https://hub.docker.com/_/mysql/)<br><br>
~~~ shell
docker pull mysql 
~~~
![docker pull]({{site.url}}/images/docker-pull.png "Ran Successfully")<br><br>
4. Now we will create the container who will have MySQL running
    1. ~~~ shell
    docker run -p 3306:3306 -p 33060:33060 -v /home/leogaller/Documents/cursos/pece-poli/disciplina/"Arquitetura de BI e Big Data":/home/data --name mysql-poli-1 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:latest
       ~~~
       ![docker run]({{site.url}}/images/docker-run-command.png "Ran Successfully")
       Let's see what each part of the command is doing:<br>
          ```docker run``` : Docker runs processes in isolated containers. A container is a process which runs on a host. [Reference](https://docs.docker.com/engine/reference/run/)<br>
          ``` -p 3306:3306 -p 33060:33060 ``` : We are telling to the container that we want the host port 3306 to be mapped to the container port 3306. With this will be able to access it from the host.<br>
          ```-v /home/leogaller/Documents/cursos/pece-poli/disciplina/"Arquitetura de BI e Big Data":/home/data``` : In this one, I'm telling to the container that I want to share a volume(directory) with the container, in which it will be created as ```/home/data``` **_Remember to replace to the folder in your computer that you want to share with the container_**.<br>
          ```--name mysql-poli-1```: This is the name that I want the container to have.<br>
          ```-e MYSQL_ROOT_PASSWORD=123456```: This parameter is extremely important because with this one you will be able to access MySQL from workbench.<br>
          ```-d```: Run this container in detached mode. [Detached mode](https://docs.docker.com/engine/reference/run/#detached--d).<br>
          ```mysql:latest```: Telling which image version to use.<br>
    2. Verifiy that the container is running<br>
    ~~~ shell
    docker ps
    ~~~
    ![docker ps]({{site.url}}/images/docker-ps.png)<br><br>

5. Now that we saw that the container is running correctly we need to get it IP to use in workbench
    1. Let's check for the network that docker created to find this container.<br>
    ```docker network list```
    ![docker network list]({{site.url}}/images/docker-network-list.png)
    2. You can the IP of the container inspecting the network *bridge*, you will its IP in the parameter IPv4Address
    ```docker network inspect bridge```
    ![docker network inspect]({{site.url}}/images/docker-net-inspect-full.png)
    Focusing in the important part<br>
    ![docker network inspect container]({{site.url}}/images/docker-net-insp-container.png)
    The IP we have is *172.17.0.2*, save it for later.<br><br>

6. Install Workbench from [here](https://dev.mysql.com/downloads/workbench/). Correctly select your operational system. In my case it is an Ubuntu Linux.
    ![Install workbench]({{site.url}}/images/mysql-ubuntu-my-version.png)<br><br>

7. After the installation is complete lets connect to the container
    1. Initial workbench screen<br>
    ![Initial workbench]({{site.url}}/images/initial-screen-workbench.png)
    2. Set a new connection, see that I gave a useful nume and in the hostname I placed the IP that I get from the network inspect. The password you created you will need to save it to a keychain for security.<br>
    ![Set connection]({{site.url}}/images/set-conn.png)
    3. Save the password to the key chain(it is the same password that you set in the parameter **MYSQL_ROOT_PASSWORD**)<br>
    ![Password to the keychain]({{site.url}}/images/password-keychain.png)
    4. Test the connection(If you did everything correctly it will be a successful connection.:D )
    ![Successful connection]({{site.url}}/images/test-conn.png)
    5. Click OK <br><br>

8. Now you will be able to see the newly created connection.<br>
![Successful connection]({{site.url}}/images/new-conn.png)<br><br>

9. Access the new connection clicking on the icon.<br>
![All working]({{site.url}}/images/all-working.png)<br><br>

10. When you are not using, stop the container(remember to get the container ID using docker ps).
```docker container stop <CONTAINER-ID>```
![Docker stop]({{site.url}}/images/docker-stop.png.png)<br><br>

11. When you wish to go back where you stopped, remember to restart your container. You do not need to run ```docker run``` now you will use ```docker container start```.<br>
    1. See your stopped container<br>
    ```docker ps -a```
    2. Restart the container
    ```docker container start <CONTAINER ID / OR NAME>```
    ```docker container start mysql-poli-1```

## Conclusion

Instead of downloading a huge software like VirtualBox or VMWare Player, and then a 8g image, just use docker. It will be faster and lightweight.
I hope you enjoy this small tool!

Be safe!
</div>