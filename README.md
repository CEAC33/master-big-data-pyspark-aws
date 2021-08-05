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






