---
layout: post
title:  "Ajuste do Spark para Distorção de Dados e Baixo Paralelismo"
date:   2022-09-01 21:38:31 -0300
categories: Spark
author:
- Leonardo Galler
meta: "Spark"
lang: pt
permalink: /pt/ajuste-spark-distorcao-dados-baixo-paralelismo/
---
<div style="text-align: justify" markdown="1">

![Apache Spark](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Apache_Spark_logo.svg/128px-Apache_Spark_logo.svg.png "A principal ferramenta para engenharia de dados!")

O Apache Spark é a ferramenta de facto para engenharia de dados, você pode confirmar isso apenas olhando para as empresas que confiam no Spark para lidar com seus esforços de engenharia de dados.

# Mas...
Pela quantidade de linguagens e tipos de aplicações que o Spark pode lidar, você pode esperar que algumas dificuldades surjam. E os principais problemas estão relacionados à **Distorção de Dados** e **Baixo Paralelismo**, e esses são os problemas em que vamos focar agora.

## Definindo os problemas
1. **Distorção de Dados**: <br>
  ![Distorção de Dados]({{site.url}}/images/data-skew.png "A definição estatística")<br>
Em termos estatísticos, uma distorção de dados refere-se à distribuição de valores que se torna ou fica desigual, como pode ser visto na primeira imagem.
A distorção de dados em sistemas computacionais para processamento de dados normalmente é causada por transformações aplicadas aos dados. Algumas dessas transformações são *Join, groupBy* e *orderBy*.<br><br>
    ![Distorção de Dados no Spark]({{site.url}}/images/skew-park.png "Referência visual de distorção de dados no Spark")<br>
Esta situação frequentemente acontece quando você está tentando fazer join de tabelas que não estão bem distribuídas nos nós do cluster, isso pode fazer com que algumas partições se tornem muito maiores que as outras, fazendo com que o Spark não processe adequadamente os dados em paralelo.

2. **Baixo Paralelismo:**
O processamento do Spark não usará totalmente os recursos do cluster até que o nível de paralelismo para cada operação seja alto o suficiente. Por essa razão, a principal fonte de baixo nível de paralelismo é a distorção de dados. Sabemos que a distorção de dados está diretamente conectada às partições e causa baixo paralelismo.<br><br>
![Baixo Paralelismo no Spark]({{site.url}}/images/low-parallelism.png "Apenas 2 tarefas processando 128 partições")<br>
No exemplo acima, podemos ver que apenas 2 executores estão processando 128 partições, mesmo que existam 12 executores disponíveis, mas não foram utilizados para processar os dados.
O baixo paralelismo faz com que o tempo do estágio de execução mais longa seja o gargalo de todo o processamento.

## Identificando o problema
**Como saber se tenho distorção de dados?**<br>
Você pode obter evidências de:
1. Executando contagens nas partições do dataframe;
2. Verificando a UI Web do SparkContext da sua aplicação e procurando por tarefas e estágios que estão demorando mais que os outros para terminar.

### Executando contagens nas partições do dataframe
Depois de ler os dados para um dataframe chamado 'df', você pode chamar a função [spark_partition_id](https://spark.apache.org/docs/3.1.1/api/python/reference/api/pyspark.sql.functions.spark_partition_id.html). Esta função quando chamada determina a(s) chave(s) das partições em um dataframe.
Encontre abaixo um comando de exemplo para encontrar o número de partições e plotá-lo usando notebooks jupyter:</div>

```python
df_partition_counts = df.groupBy(spark_partition_id()) \
    .count() \
    .orderBy(desc("count"))
```

<div style="text-align: justify" markdown="1">
Você pode ver abaixo um exemplo de saída:<br>

*[O restante do post continuaria com as soluções e exemplos técnicos...]*</div> 