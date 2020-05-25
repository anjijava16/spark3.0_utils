# spark3.0_utils
Apache Spark echo system is about to explode — Again! — this time with Sparks newest major version 3.0.

Apache Spark 3.0 Preview was released on 2019-Nov-08 and available for experimentation since then.

# Download: 
   https://archive.apache.org/dist/spark/spark-3.0.0-preview2/


Spark 3.0 is said to perform 17x faster compared with current versions on the TPCDS benchmark which is pretty impressive.

3.0 features :
 
 1.Dynamic Partition Pruning
 
 3.Binary files data source
 
 3.Spark on k8s
  
 4.RPC communication between driver and executors
 
 5.RAPIDS
 
 


# Programming Language Support
  Spark 3.0 will move to Python3 and Scala version is upgraded to version 2.12. In addition it will fully support JDK 11. Python 2.x is heavily deprecated

  Apache Spark 3.0 runs on Java 8/11, Scala 2.12, Python 2.7+/3.4+ and R 3.1+.

  Java 8 prior to version 8u92 support is deprecated as of Spark 3.0.0.

  Python 2 and Python 3 prior to version 3.6 support is deprecated as of Spark 3.0.0.

  R prior to version 3.4 support is deprecated as of Spark 3.0.0.

  For the Scala API, Spark 3.0.0-preview uses Scala 2.12.

  You will need to use a compatible Scala version (2.12.x).
  

# Binary files data source
  val df = spark.read.format(“binaryFile”)
```        
     The above will read binary files and converts each one to a single row that contains the raw content and metadata of the file. The DataFrame will contain the following columns and possibly partition columns:
        path: StringType
        modificationTime: TimestampType
        length: LongType
        content: BinaryType
        writing back a binary DataFrame/RDD is currently not supported.
```

# DPP : Dynamic Partition Pruning
 Apache Spark 3.0 brought the concept of Dynamic Partition Pruning (DPP) which is a key performance improvement for SQL analytics workloads that in term can make integration with BI tools much better.

 The concept behind Dynamic Partition Pruning (DPP) is to apply the filter set on the dimension table — mostly small and used in a broadcast hash join — directly on the fact table so it could skip scanning unneeded partitions.

 https://databricks.com/session_eu19/dynamic-partition-pruning-in-apache-spark
 In data analytics frameworks such as Spark it is important to detect and avoid scanning data that is irrelevant to the executed query, an optimization which is known as partition pruning. Dynamic partition pruning occurs when the optimizer is unable to identify at parse time the partitions it has to eliminate. In particular, we consider a star schema which consists of one or multiple fact tables referencing any number of dimension tables.
  In such join operations, we can prune the partitions the join reads from a fact table by identifying those partitions that result from filtering the dimension tables. In this talk we present a mechanism for performing dynamic partition pruning at runtime by reusing the dimension table broadcast results in hash joins and we show significant improvements for most TPCDS queries.


# Spark SQL: Adaptive Execution
  This feature helps in where statistics on the data source do not exists or are in accurate. So far Spark had some optimizations which could be set only in the planning phase and according to the statistics of data (e.g. the ones captured by the ANALYZE command when deciding weather to perform a Broadcast-hash join over an expensive Sort-merge join. In cases in which these statistics are missing or not accurate BHJ might not kick in. with adaptive execution in Spark 3.0 spark can examine that data at runtime once he had loaded it and opt-in to BHJ at runtime even it could not detect it on the planning phase.
  
# Growing integration with Apache Arrow data format
  Apache Arrow: Apache Arrow is an in-memory columnar data structure for efficient analytical operations. Its has benefits like being cross-language platform, performing zero-copy streaming messaging and interprocess communications without serialization costs which often occur with other systems.

# Better Kubernetes Integration
  Spark support for Kubernetes is relatively not matured in the 2.x version and difficult to use in production and performance was lacking in compare with the YARN cluster manager. Spark 3.0 introduces new shuffle service for Spark on Kubernetes that will allow dynamic scale up and down (more precisely out and in)
  Spark 3.0 also supports GPU support with pod level isolation for executors which makes scheduling more flexible on a cluster with GPUs. Spark authentication on Kubernetes also has some goodies
  
# YARN Features
  Spark 3.0 can auto discover GPUs on a YARN cluster and schedule tasks specifically on nodes with GPUs.    
   
# ACID Transactions with Delta Lake
   Delta Lake is an open-source storage layer that brings ACID transactions to Apache Spark 3.0 and through easy implementation and upgrading of existing Spark applications, it brings reliability to Data Lakes. It announced to join the Linux foundation to grow its community.
   https://docs.databricks.com/delta/quick-start.html

# Graph features:
  Spark 3.0 introduces a whole new module named SparkGraph with major features for Graph processing. 
  These features include the popular Cypher query language developed by Neo4J which is a SQL like for graphs, the Property Graph Model processed by this language and Graph algorithms. This integration is something Neo4J worked on for several years and it’s named Morpheus (formerly named Cypher for Spark) but as said will be named SparkGraph inside the spark components.
  https://www.youtube.com/watch?v=mEYvEF_2fDc

# Pandas UDFs and Python Type Hints in the Upcoming Release of Apache Spark 3.0
 Pandas UDFs were introduced in Spark 2.3, see also Introducing Pandas UDF for PySpark. Pandas is well known to data scientists and has seamless integrations with many Python libraries and packages such as NumPy, statsmodel, and scikit-learn, and Pandas UDFs allow data scientists not only to scale out their workloads, but also to leverage the Pandas APIs in Apache Spark.

 The user-defined functions are executed by:

 Apache Arrow, to exchange data directly between JVM and Python driver/executors with near-zero (de)serialization cost.
Pandas inside the function, to work with Pandas instances and APIs.

 https://databricks.com/blog/2020/05/20/new-pandas-udfs-and-python-type-hints-in-the-upcoming-release-of-apache-spark-3-0.html 
 
 # Reference Links:
   http://blog.madhukaraphatak.com/categories/spark-three/
   http://apache-spark-developers-list.1001551.n3.nabble.com/Spark-3-0-preview-release-feature-list-and-major-changes-td28050.html
   
  
    
