# Trino local setup for UDF testing


## Steps to Run Trino local with UDFs jar

1. comment all UDF except testing one from `UDFunctionsPlugin`
2. build the UDF jar

    ```shell
    bazel build //presto-udfs:build-presto-udfs_with_mvn_cache_filler
    ```

3. copy the jar in `plugin/udfs`
4. run docker containers

    ```shell
    docker-compose up -d
    ```

   if want to pass configs

    ```shell
    docker-compose -e MYSQL_ROOT_PASSWORD=myrootpass -e MYSQL_DATABASE=mycustomdb up -d
    ```

5. stop the container after testing

    ```shell
    docker-compose down
    ```

## steps to run queries

1. install Trino cli

    ```shell
    brew install trino    
    ```

2. connect to Trino

    ```shell
    trino --server http://localhost:8080 --catalog mysql --schema mydb
    ```

3. queries to test UDF, for example

    ```shell
    select parse_user_agent('Mozilla/5.0 (Linux\; Android 6.0\; Nexus 6 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/46.0.2490.76 Mobile Safari/537.36');
    ```

## setup for different trino-version with mysql connector

> Currently this repo jars support Trino-version 380.

If we want to change the Trino-version then:

- create a branch with `trino-version` name
- update the `plugin/mysql` jars
  - to get the right set of jars either download from Trino machine or build from code
  - or use https://jar-download.com/artifacts/io.Trino/
  - make sure jars and image tag are in sync
- test it by docker-compose up

## setup with hive

> one can try setup add hive catalog if host machine have good resources