# Teste para Engenheiro de Dados na Semantix

[![Logo Semantix](https://github.com/paaarx/semantix/blob/master/semantix_logo.jpg "Logo Semantix")](https://github.com/paaarx/semantix/blob/master/semantix_logo.jpg "Logo Semantix")

------------

## Questões

Qual o objetivo do comando **cache** em Spark?
```
O objetivo é otimizar o desempenho de uma operação persistindo (caching) o resultado em memória, para que seja reutilizado futuramente, de forma a evitar o overhead ao realizar consultas em disco.
Exemplo: Para realizar a contagem da palavra "spark" e contagem de hashtags, podemos inicialmente fazer uma transformação de todo o conteúdo do arquivo em minúsculo, realizar o cache dele, então podemos utilizar esse RDD em cache para fazer a contagem de palavras e de hashtags, evitando que seja necessário executar duas vezes (uma para a palavra e outra para hashtag) a operação de transformar em minúsculo o conteúdo do arquivo.
```

O mesmo código implementado em Spark é normalmente mais rápido que a implementação equivalente em MapReduce. Por quê?
```
Pois em MapReduce após as operações serem realizadas elas são persistidas em disco, então nas operações subsequentes, novamente deverá ler do disco esses dados, e no Spark não ocorre isso, os dados intermediários podem ser persistidos em memória e utilizados nas operações subsequentes, então há um ganho de performance, pois o throughput da leitura em memória é muito maior que em disco.
```

Qual é a função do **SparkContext**?
```
É criar uma conexão com o cluster Spark, e pode ser usado para criar RDDs, accumulators e broadcast variables no cluster.
Observação: Pode-se ter apenas um SparkContext ativo por JVM.
```

Explique com suas palavras o que é **Resilient Distributed Datasets** (RDD).
```
RDD é uma abstração para processamento distribuído, como uma manual de instruções do que deve ser executado, onde o retorno é uma coleção imutável de objetos.
Quanto as palavras da sigla, Resilient por ser tolerante a falhas, ou seja, caso ocorra algum problema em uma partição ele consegue recomputar o que estava realizando, Distributed pois acessa dados em diversos nodes e Dataset pois retorna a coleção imutável de objetos.
```

**GroupByKey** é menos eficiente que **reduceByKey** em grandes dataset. Por quê?
```
Pois o GroupByKey mapeia e então envia todo o conteúdo obtido para o shuffling nos demais clusters, e o reduceByKey antes de enviar para o shuffling, ele mapeia e realiza um agrupamento prévio (um "pré-reduce"), então passa para os clusters apenas a contagem total.
Exemplo: Quero somar quantas incidências há em SP e quantas no RJ.
No cluster 1 temos, (1, SP), (1, SP), (1, SP), (1, RJ).
No cluster 2 temos, , (1, SP), (1, RJ), (1, RJ).
O GroupByKey enviaria para o Cluster 3 (1, SP), (1, SP), (1, SP), (1, SP) e para o Cluster 4 (1, RJ), (1, RJ), (1, RJ).
O reduceByKey enviaria para o Cluster 3 (4, SP) e para o Cluster 4 (3, RJ).
Conforme demonstrado acima, o GroupByKey enviaria os 7 registros (4 para um e 3 para outro) e o reduceByKey enviaria 2 (1 para cada).
```

Explique o que o código Scala abaixo faz.
```scala
1. val textFile = sc.textFile ("hdfs://...")
2. val counts = textFile . flatMap (line => line.split( " " ))
3.     .map (word => ( word , 1 ))
4.     .reduceByKey(_+_)
5. counts.saveAsTextFile( "hdfs://..." )
```

```
1. Lê um arquivo de texto do HDFS e atribui a variável textFile.
2. Salva o retorno das operações na variável counts. Realiza um flatmap (aplica uma transformação em cada elemento) no texto e então divide as palavras usando como delimitador o espaço.
3. Faz um map (gera o par chave, valor) de quantas palavras encontrou através da divisão anterior.
4. Para cada chave (word) ele realiza a soma.
5. Salva o resultado do counts no HDFS como texto.
```

------------

## HTTP requests to the NASA Kennedy Space Center WWW server

**Fonte oficial do dateset:** [http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html](http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html "http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html")

**Dados:**
- [NASA_access_log_Aug95.gz](NASA_access_log_Aug95.gz)
- [NASA_access_log_Jul95.gz](NASA_access_log_Jul95.gz)

**Sobre o dataset:** Esses dois conjuntos de dados possuem todas as requisições HTTP para o servidor da NASA Kennedy Space Center WWW na Flórida para um período específico.

Os logs estão em arquivos ASCII com uma linha por requisição com as seguintes colunas:
- **Host fazendo a requisição.** Um hostname quando possível, caso contrário o endereço de internet se o nome não puder ser identificado.
- **Timestamp** no formato "DIA/MÊS/ANO: HH: MM: SS TIMEZONE" (sem espaço entre HHMMSS e os dois pontos)
- **Requisição (entre aspas)**
- **Código do retorno HTTP**
- **Total de bytes retornados**

### Questões
Responda as seguintes questões devem ser desenvolvidas em Spark utilizando a sua linguagem de preferência.

* 1. Número de hosts únicos.
* 2. O total de erros 404.
* 3. Os 5 URLs que mais causaram erro 404.
* 4. Quantidade de erros 404 por dia.
* 5. O total de bytes retornados.

O código com as respostas pode ser obtido no Notebook [semantix_teste_spark.ipynb](semantix_teste_spark.ipynb) ou pelo Notebook hospedado no [DataBricks](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/7595947905727238/1667145015670894/2733465045966151/latest.html)
