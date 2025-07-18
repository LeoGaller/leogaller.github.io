---
layout: post
title:  "MySQL com Workbench usando Docker"
date:   2023-06-15 22:00:00 -0300
categories: Docker
author:
- Leonardo Galler
meta: "MySQL"
lang: pt
permalink: /pt/mysql-workbench-docker/
---
<div style="text-align: justify" markdown="1">

![MySQL](https://www.mysql.com/common/logos/logo-mysql-170x115.png "Leve e Poderoso!")

Às vezes, em seus esforços para aprender novas tecnologias, você tem a necessidade de testar novas ferramentas e aprender novas habilidades, como o uso de bancos de dados e SQL.

# Começando bem
Com este post, gostaria de fornecer a qualquer pessoa uma maneira de começar rapidamente a desenvolver e usar MySQL e Workbench em seus estudos.

## Ferramentas
1. **MySQL:**<br>
![MySQL Inside](https://www.mysql.com/common/logos/powered-by-mysql-125x64.png "Banco de dados leve")<br>
> MySQL é o banco de dados de código aberto mais popular do mundo. Com sua performance comprovada, confiabilidade e facilidade de uso, o MySQL se tornou a escolha líder de banco de dados para aplicações baseadas na web, cobrindo toda a gama desde projetos pessoais e sites, via e-commerce e serviços de informação, até propriedades web de alto perfil incluindo Facebook, Twitter, YouTube, Yahoo! e muitos mais.<br>
Fonte: [Página Oficial do MySQL](https://www.mysql.com/)

2. **MySQL Workbench:**<br>
![MySQL Workbench](https://www.mysql.com/common/images/products/MySQL_Workbench_Mainscreen_Windows.gif "Ferramenta de Dados")<br>
> MySQL Workbench é uma ferramenta visual unificada para arquitetos de banco de dados, desenvolvedores e DBAs. O MySQL Workbench fornece modelagem de dados, desenvolvimento SQL e ferramentas de administração abrangentes para configuração de servidor, administração de usuário, backup e muito mais. O MySQL Workbench está disponível no Windows, Linux e Mac OS X.<br>
Fonte: [Página Oficial do MySQL Workbench](https://www.mysql.com/products/workbench/)

3. **Docker:**<br>
![Docker](https://www.docker.com/wp-content/uploads/2022/03/horizontal-logo-monochromatic-white.png "Docker")<br>
> Docker é uma plataforma aberta para desenvolver, enviar e executar aplicações. O Docker permite separar suas aplicações de sua infraestrutura para que você possa entregar software rapidamente. Com o Docker, você pode gerenciar sua infraestrutura da mesma forma que gerencia suas aplicações. Aproveitando as metodologias do Docker para envio, teste e implantação de código rapidamente, você pode reduzir significativamente o atraso entre escrever código e executá-lo em produção.<br>
Fonte: [Página Oficial do Docker](https://docs.docker.com/get-started/overview/)

## Identificando o problema
**_Preciso de um banco de dados e uma ferramenta para modelagem de dados e consultas usando SQL!_**<br>
Para começar rapidamente seus estudos ou análises em qualquer uma dessas ferramentas, você deve conseguir tê-las em minutos e não horas ou ainda pior manipulando enormes imagens de VM.

### Passo a passo
1. Instale o docker e verifique se está funcionando.
  * No [Windows](https://docs.docker.com/desktop/install/windows-install/)
  * No [Mac](https://docs.docker.com/desktop/install/mac-install/); Para Mac você terá a opção de chip, verifique qual é o seu antes.
  * No [Linux](https://docs.docker.com/desktop/install/linux-install/)<br><br>

2. Abra o terminal<br><br>
3. Baixe a imagem docker para [MySQL](https://hub.docker.com/_/mysql/)<br><br>
~~~ shell
docker pull mysql 
~~~
![docker pull]({{site.url}}/images/docker-pull.png "Executado com Sucesso")<br><br>

*[O restante do post continuaria com os passos detalhados de configuração...]*</div> 