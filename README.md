# Trino local setup


## setup

> Currently this repo support trino-version 380. If we want to change the trino-version then 

- create a branch with trino-version name
- update the plugin/mysql jars
- test it by docker-compose up

## Run


1. comment all udfs
2. docker-compose up -d
3. brew install trino
4. trino --server http://localhost:8080 --catalog mysql --schema mydb
5. queries to test udf

```
select parse_user_agent('Mozilla/5.0 (Linux\; Android 6.0\; Nexus 6 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/46.0.2490.76 Mobile Safari/537.36');
```
