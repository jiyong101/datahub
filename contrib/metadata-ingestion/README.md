# datahub Ingestion Tool


## Introduction

some tool to ingestion [jdbc-database-schema] and [etl-lineage] metadata.

i split the ingestion procedure to two part: [datahub-producer] and different [metadata-generator]


## Roadmap

- [X] datahub-producer load json avro data.
- [X] add lineage-hive generator
- [X] add dataset-jdbc generator[include [mysql, mssql, postgresql, oracle] driver]
- [ ] enhance dataset-jdbc generator [hive-driver]
- [ ] enhance lineage-jdbc generator to lazy iterator mode.
- [ ] add lineage-oracle generator
- [ ] enchance avro parser to show error information 



## Quickstart
1.  install nix and channel

```
  sudo install -d -m755 -o $(id -u) -g $(id -g) /nix
  curl https://nixos.org/nix/install | sh
  
  nix-channel --add https://nixos.org/channels/nixos-20.03 nixpkgs
  nix-channel --update nixpkgs
```

2. load json data to datahub

```
    cat sample/mce.json.dat | bin/datahub-producer.hs config
```

3. parse hive sql to  datahub
```
    ls sample/hive_*.sql | bin/lineage_hive_generator.hs | bin/datahub-producer.hs config
```

4. load jdbc schema(mysql, mssql, postgresql, oracle) to datahub
```
    bin/dataset-jdbc-generator.hs | bin/datahub-producer.hs config
```

## Reference

- hive/presto/vertica SQL Parser  
  uber/queryparser [https://github.com/uber/queryparser.git]
  
- oracle procedure syntax  
  https://docs.oracle.com/cd/E11882_01/server.112/e41085/sqlqr01001.htm#SQLQR110
  
- postgresql procedure parser  
  SQream/hssqlppp [https://github.com/JakeWheat/hssqlppp.git]
