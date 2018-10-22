# 存储卷

## 运行存储卷容器
```bash
$ docker run -d --volume /var/lib/cassandra/data --name cass-shared alpine echo Data Container
```

## 运行cassandra数据库服务端cass1
```bash
docker run -d --volumes-from cass-shared --name cass1 cassandra:latest
```

## 运行cassandra数据库客户端
```bash
docker run -it --link cass1:cassandra --rm cassandra:latest cqlsh cassandra
```

```bash
cqlsh> SELECT * FROM system_schema.keyspaces;

 keyspace_name      | durable_writes | replication
--------------------+----------------+-------------------------------------------------------------------------------------
        system_auth |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '1'}
      system_schema |           True |                             {'class': 'org.apache.cassandra.locator.LocalStrategy'}
 system_distributed |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '3'}
             system |           True |                             {'class': 'org.apache.cassandra.locator.LocalStrategy'}
      system_traces |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '2'}

(5 rows)


cqlsh> CREATE KEYSPACE test
  WITH REPLICATION = { 
   'class' : 'SimpleStrategy', 
   'replication_factor' : 1 
  };


cqlsh> SELECT * FROM system_schema.keyspaces;

 keyspace_name      | durable_writes | replication
--------------------+----------------+-------------------------------------------------------------------------------------
               test |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '1'}
        system_auth |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '1'}
      system_schema |           True |                             {'class': 'org.apache.cassandra.locator.LocalStrategy'}
 system_distributed |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '3'}
             system |           True |                             {'class': 'org.apache.cassandra.locator.LocalStrategy'}
      system_traces |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '2'}

(6 rows)

cqlsh> quit
```

## 删除正在运行的cass1容器
```bash
$ docker rm -vf cass1
```

## 运行cassandra数据库服务端cass2
```bash
docker run -d --volumes-from cass-shared --name cass2 cassandra:latest
```

## 运行cassandra数据库客户端
```bash
docker run -it --link cass2:cassandra --rm cassandra:latest cqlsh cassandra
```

```bash
cqlsh> SELECT * FROM system_schema.keyspaces;

 keyspace_name      | durable_writes | replication
--------------------+----------------+-------------------------------------------------------------------------------------
               test |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '1'}
        system_auth |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '1'}
      system_schema |           True |                             {'class': 'org.apache.cassandra.locator.LocalStrategy'}
 system_distributed |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '3'}
             system |           True |                             {'class': 'org.apache.cassandra.locator.LocalStrategy'}
      system_traces |           True | {'class': 'org.apache.cassandra.locator.SimpleStrategy', 'replication_factor': '2'}

(6 rows)

cqlsh> quit
```

## 删除容器
```bash
$ docker rm -vf cass2 cass-shared
```

## 参考资料
* [alpine](https://hub.docker.com/_/alpine/)
* [cassandra](https://hub.docker.com/_/cassandra/)
* [Cassandra](https://cassandra.apache.org)
* [CREATE KEYSPACE](https://docs.datastax.com/en/cql/3.3/cql/cql_reference/cqlCreateKeyspace.html)
* [Querying from system.schema_keyspaces generates code=2200 [Invalid query]](https://dba.stackexchange.com/questions/149977/querying-from-system-schema-keyspaces-generates-code-2200-invalid-query)