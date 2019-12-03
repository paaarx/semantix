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
resposta_aqui
```

Qual é a função do **SparkContext**?
```
resposta_aqui
```

Explique com suas palavras o que é **Resilient Distributed Datasets** (RDD).
```
resposta_aqui
```

**GroupByKey** é menos eficiente que **reduceByKey** em grandes dataset. Por quê?
```
resposta_aqui
```

Explique o que o código Scala abaixo faz.
```scala
val textFile = sc . textFile ( "hdfs://..." )
val counts = textFile . flatMap ( line => line . split ( " " ))
. map ( word => ( word , 1 ))
. reduceByKey ( _ + _ )
counts . saveAsTextFile ( "hdfs://..." )
```

```
resposta_aqui
```

------------

## HTTP requests to the NASA Kennedy Space Center WWW server

**Fonte oficial do dateset:** [http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html](http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html "http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html")

**Dados:**
- [Jul 01 to Jul 31, ASCII format, 20.7 MB gzip compressed , 205.2 MB. (ftp://ita.ee.lbl.gov/traces/NASA_access_log_Jul95.gz)](ftp://ita.ee.lbl.gov/traces/NASA_access_log_Jul95.gz "Jul 01 to Jul 31, ASCII format, 20.7 MB gzip compressed , 205.2 MB.")
- [Aug 04 to Aug 31, ASCII format, 21.8 MB gzip compressed , 167.8 MB. (ftp://ita.ee.lbl.gov/traces/NASA_access_log_Aug95.gz)](ftp://ita.ee.lbl.gov/traces/NASA_access_log_Aug95.gz "Aug 04 to Aug 31, ASCII format, 21.8 MB gzip compressed , 167.8 MB.")

**Sobre o dataset:** Esses dois conjuntos de dados possuem todas as requisições HTTP para o servidor da NASA Kennedy Space Center WWW na Flórida para um período específico.

Os logs estão em arquivos ASCII com uma linha por requisição com as seguintes colunas:
- **Host fazendo a requisição.** Um hostname quando possível, caso contrário o endereço de internet se o nome não puder ser identificado.
- **Timestamp** no formato "DIA/MÊS/ANO: HH: MM: SS TIMEZONE" (sem espaço entre HHMMSS e os dois pontos)
- **Requisição (entre aspas)**
- **Código do retorno HTTP**
- **Total de bytes retornados**

### Questões
Responda as seguintes questões devem ser desenvolvidas em Spark utilizando a sua linguagem de preferência.

1. Número de hosts únicos.
```python
print('resposta_aqui')
```

2. O total de erros 404.
```python
print('resposta_aqui')
```

3. Os 5 URLs que mais causaram erro 404.
```python
print('resposta_aqui')
```

4. Quantidade de erros 404 por dia.
```python
print('resposta_aqui')
```

5. O total de bytes retornados.
```python
print('resposta_aqui')
```
