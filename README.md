# Apache Hive UDF Repository

A list of user defined functions are collected here for Hive and Spark SQL.

## For Development:

1. Build the JAR:
    ```
    mvn package
    ```

2. Start Hive CLI with the JAR in your classpath:
    ```
    export HADOOP_CLASSPATH=target/df-hiveudf-1.0-SNAPSHOT.jar ; hive
    ```

3. Execute:
    ```
    create temporary function my_lower as 'com.datafibers.hiveudf.CustomLower';
    ```

4. Execute:
    ```
    select my_lower("UPPER CASE LETTERS");
    ```

## For Deployment:

1. In shell commandline, create a permanent function:
    ```c
    hdfs dfs -mkdir /apps/hive/functions
    hdfs dfs -chown hive:hive /apps/hive/functions
    cp df-hiveudf-1.0-SNAPSHOT.jar /tmp
    hdfs dfs -put -f /tmp/df-hiveudf-1.0-SNAPSHOT.jar /apps/hive/functions
    ```
2. In beeline, create/register the function
    ```c
    CREATE FUNCTION my_lower AS 'com.datafibers.hiveudf.CustomLower' USING JAR 'hdfs:////apps/hive/functions/df-hiveudf-1.0-SNAPSHOT.jar';
    ```

3. After that, you can use the functions like hive build-in functions.

## For Streaming Function
For streaming function by python, follow steps below.
```
hdfs dfs -mkdir /apps/hive/scripts
hdfs dfs -put hive_udf_addfile.py /apps/hive/scripts
hive -f hive_udf_addfile.sql
```

