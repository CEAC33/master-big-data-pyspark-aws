# master-big-data-pyspark-aws

## Intro

### Application of PySpark
- Streaming Data
- Machine Learning
- Batch Data
- ETL Pipelines
- Full load and Replication on going

## Introduction to Hadoop, Spark Ecosystem and Architectures

### Why Spark?
- Speed
- Distributed
- Advanced Analytics
- Real Time
- Powerful Caching
- Fault Tolerant
- Deployment

### Hadoop Ecosystem
- HDFS - Hadoop Distributed File System, distributed storage
- YARN - Like the OS, allocate resources
- Map Reduce - A technique for mapping and reducing the data
- SPARK - Much more reliable, faster an durable approach for mapping and reduce functionality

![Screenshot 2021-08-03 at 17 40 31](https://user-images.githubusercontent.com/51218415/128095423-76aca077-954c-4d4e-b172-1b2177567c93.png)

![Screenshot 2021-08-03 at 17 43 37](https://user-images.githubusercontent.com/51218415/128095683-c6a8e915-38f4-4b50-bf55-059a132019a5.png)

### Spark Architecture and Ecosystem

![Screenshot 2021-08-03 at 20 15 24](https://user-images.githubusercontent.com/51218415/128106330-88efdb0b-4874-4d90-96e1-23cd67ddbc56.png)

![Screenshot 2021-08-03 at 20 18 10](https://user-images.githubusercontent.com/51218415/128106635-844bf9d3-08df-47b4-ae05-c4bf191d6344.png)

### DataBricks SignUp

https://community.cloud.databricks.com/

### Create a DataBricks Notebook

https://community.cloud.databricks.com/

Go to **Compute**:

<img width="200" alt="Screenshot 2021-08-03 at 21 06 14" src="https://user-images.githubusercontent.com/51218415/128110345-75a69b9a-3262-4b7d-aa51-d79330380be4.png">

**Create Cluster**
- **Cluster Name:** PySpark Cluster
- **Databricks Runtime Version:** 8.1
- Create Cluster

Go to **Create**:

<img width="200" alt="Screenshot 2021-08-03 at 21 15 57" src="https://user-images.githubusercontent.com/51218415/128111138-ab8262c6-4b58-49df-bbf1-8e16090493f4.png">

**Create Notebook:**
- Click on **New Notebook**
- **Name:** Hello World
- **Default Language:** Python
- **Cluster:** PySpark Cluster

`print("Hello World!")`

### Download Spark and Dependencies

- https://java.com/en/download/
- https://www.python.org/
- https://spark.apache.org/downloads.html
- https://github.com/cdarlint/winutils - Select your hadoop version and download `bin/winutils.exe`

## Spark RDDs

### Spark RDDs

**Spark RDDs**
- RDD is the spark's core abstraction which stands for Resilient Distributed Dataset
- RDD is the inmutable distributed collection of objects
- Internally spark distributes the data in RDD, to different nodes acorss the cluster to achieve parallelization

**Transformations and Actions**
- Transformations create a new RDD from an existing one
- Actions return a value to the driver program after running a computation on the RDD
- All transformations in Spark are lazy
- Spark only triggers the data flow when there's an action

### Creating Spark RDD

Go to Data > Create Table

<img width="731" alt="Screenshot 2021-08-05 at 15 59 31" src="https://user-images.githubusercontent.com/51218415/128420447-30521d2d-d3f3-41f9-a1ba-495923df8fd0.png">

Create a txt file `sample.txt`

```
1 2 3 4 5
3 4 5 66 77
12 43 6 7 8
12 12 33
```

And upload it 

<img width="659" alt="Screenshot 2021-08-06 at 0 05 01" src="https://user-images.githubusercontent.com/51218415/128458675-fcbb3cf3-75ed-4ff9-b28a-57b71b6b00bd.png">

Then go to `DBFS` 
- FileStore > tables > sample.txt

<img width="1147" alt="Screenshot 2021-08-06 at 0 06 16" src="https://user-images.githubusercontent.com/51218415/128458762-14cd60f7-fb8e-4124-9db4-730ae838dbfe.png">

Return to your notebook

```python
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("Read File")
sc = SparkContext.getOrCreate(conf=conf)
text = sc.textFile('/FileStore/tables/sample.txt')
text.collect()
```

### RDD Map (Lambda)

**map()**
- Map is used as a maper of data from one state to other
- It will create a new RDD
- rdd.map(lambda x:x.plit())

Go your notebook

```python
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("Read File")
sc = SparkContext.getOrCreate(conf=conf)
rdd = sc.textFile('/FileStore/tables/sample.txt')
rdd.collect()
```

```python
rdd2 = rdd.map(lambda x: x.split(' '))
rdd2.collect()
```

```python
rdd3 = rdd.map(lambda x: x + " Carlos")
rdd3.collect()
```

### RDD Map (Simple Function)

```python
def foo(x):
  return x.split(' ')
  
rdd4 = rdd.map(foo)
rdd4.collect()
```

```python
def foo2(x):
  l = x.split()
  l2 = []
  for s in l:
    l2.append(int(s) + 10)
  return l2

rdd5 = rdd.map(foo2)
rdd5.collect()
```

### QUIZ

`Quiz Sample.txt`

```python
Hi how are you?
Hope you are doing
great
```

Quiz:
- Read this file in the RDD
- Write a mapper that will provide the length of each word in the following format
[[2,3,3,4], [4,3,3,5], [5]]

```python
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("Read File")
sc = SparkContext.getOrCreate(conf=conf)
rdd = sc.textFile('/FileStore/tables/Quiz_Sample.txt')

def char_counter(x):
  word_list = x.split()
  result = []
  for word in word_list:
    result.append(len(word))
  return result

result = rdd.map(char_counter)
result.collect()
```

### Solution 1 (Map)

Setup:

```python
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("Read File")
sc = SparkContext.getOrCreate(conf=conf)
rdd = sc.textFile('/FileStore/tables/Quiz_Sample.txt')
```

Solution 1:

```python
def quiz(x):
  # x -> 'great'
  l = x.split(' ') # l -> ['great']
  l2 = []
  for s in l:
    l2.append(len(s))
  return l2
  
rdd2 = rdd.map(quiz)
rdd2.collect()
```

### Solution 2 (Map)

Setup:

```python
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("Read File")
sc = SparkContext.getOrCreate(conf=conf)
rdd = sc.textFile('/FileStore/tables/Quiz_Sample.txt')
```

Solution 2:

```python
rdd3 = rdd.map(lambda x: [len(s) for s in x.split(' ')])
rdd3.collect()
```

### RDD FlatMap

**flatMap()**
- Flat Map is used as a maper of data and explodes data before final output
- It will create a new RDD
- rdd.flatMap(lambda x:x.split())

```python
# Databricks notebook source
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("FlatMap")
sc = SparkContext.getOrCreate(conf=conf)

# COMMAND ----------

rdd = sc.textFile('/FileStore/tables/sample.txt')
rdd.collect()

# COMMAND ----------

flatMappedRdd = rdd.flatMap(lambda x: x.split(" "))
flatMappedRdd.collect()
```

### RDD Filter

**filter()**
- Filter is used to remove the elements from the RDD
- It will create a new RDD
- rdd.filter(lambda: x: x != 123)

```python
# Databricks notebook source
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("FlatMap")
sc = SparkContext.getOrCreate(conf=conf)

# COMMAND ----------

rdd = sc.textFile('/FileStore/tables/sample.txt')
rdd.collect()

# COMMAND ----------

def foo(x):
  if x == '12 12 33':
    return False
  else:
    return True

rdd2 = rdd.filter(foo)
rdd2.collect()
```

### Quiz (Filter)

Use this as input file:

```
this mango company animal
cat dog ant mic laptop
chair switch mobile am charger cover
amanda any alarm ant
```

- Read this file in the RDD
- Write a filter that will remove all the words that are either starting from a or c from the rdd

```python
# Databricks notebook source
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("FlatMap Quiz")
sc = SparkContext.getOrCreate(conf=conf)

# COMMAND ----------

rdd = sc.textFile('/FileStore/tables/Quiz_Filter.txt')
rdd.collect()

# COMMAND ----------

def quiz(x):
  if x[0] in ["a", "c"]:
    return False
  else:
    return True

splitted_rdd = rdd.flatMap(lambda x: x.split(" "))
rdd2 = splitted_rdd.filter(quiz)
rdd2.collect()
```

### Solution (Filter)

```python
rdd = sc.textFile('/FileStore/tables/sample_words.txt')

# COMMAND ----------

flatMappedRdd = rdd.flatMap(lambda x: x.split(' '))

# COMMAND ----------

def filterAandC(x):
  if x.startswith('a') or x.startswith('c'):
    return False
  else:
    return True
  
filteredRdd = flatMappedRdd.filter(filterAandC)

# COMMAND ----------

filteredRdd.collect()

# COMMAND ----------

filteredRddLambda = flatMappedRdd.filter(lambda x: not (x.startswith('a') or x.startswith('c')) )

# COMMAND ----------

filteredRddLambda.collect()
```

### RDD Distinct

**distinct()**
- Distinct is used to get the distinct elements in RDD
- It will create a new RDD
- rdd.distinct()

```python
# Databricks notebook source
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("distinct")
sc = SparkContext.getOrCreate(conf=conf)

# COMMAND ----------

rdd = sc.textFile('/FileStore/tables/sample.txt')

# COMMAND ----------

rdd2 = rdd.distinct()
rdd2.collect()

# COMMAND ----------

rdd2 = rdd.flatMap(lambda x: x.split(" "))
rdd3 = rdd2.distinct()
rdd3.collect()

# COMMAND ----------

rdd.flatMap(lambda x: x.split(" ")).distinct().collect()
```

### RDD GroupByKey

**groupByKey()**
- GroupByKey is used to create groups based on Keys in RDD
- For groupByKey to work properly the data must be in format of (k,v), (k,v), (k2,v), (k2,v2)
    - Example: ("Apple",1), ("Ball",1), ("Apple",1)
- It will create a new RDD
- rdd.groupByKey()
- mapValues(list) are usually used to get the group data

```python
# Databricks notebook source
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("distinct")
sc = SparkContext.getOrCreate(conf=conf)

# COMMAND ----------

rdd = sc.textFile('/FileStore/tables/sample_words.txt')

# COMMAND ----------

rdd2 = rdd.flatMap(lambda x: x.split(' '))

# COMMAND ----------

rdd3 = rdd2.map(lambda x: (x,len(x)))
rdd3.collect()

# COMMAND ----------

rdd3.groupByKey().mapValues(list).collect()

# COMMAND ----------
```

### RDD ReduceByKey

**reduceByKey()**
- ReduceByKey is used to combine data based on Keys in RDD
- For reduceByKey to work properly the data must be in the format of (k,v), (k,v), (k2,v), (k2,v2)
    - Example: ("Apple",1), ("Ball",1), ("Apple",1)
- It will create a new RDD
- rdd.reduceByKey(lambda x, y: x + y)

```python
# Databricks notebook source
from pyspark import SparkConf, SparkContext
conf = SparkConf().setAppName("distinct")
sc = SparkContext.getOrCreate(conf=conf)

# COMMAND ----------

rdd = sc.textFile('/FileStore/tables/sample.txt')
rdd.collect()

# COMMAND ----------

rdd2 = rdd.flatMap(lambda x: x.split(' '))

# COMMAND ----------

rdd3 = rdd2.map(lambda x: (x,1))
rdd3.collect()

# COMMAND ----------

rdd3.reduceByKey(lambda x,y: x+y).collect()
```

### Quiz (Word Count)

Input file:

```
this mango company
cat mango ant animal laptop
chair switch mango am charger cover
animalany mango ant laptop laptop
this
```

- Read this file in the RDD
- Write a transformation flow that will return the word count of each word present in the file as (key, value) pair

