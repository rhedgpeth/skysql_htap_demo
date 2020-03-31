# [MariaDB](http://www.mariadb.com) SkySQL Demo Data

The purpose of this repository is to supply the schema and data to be used with a MariaDB [Hybrid Transactional/Analytical Processing (HTAP)](https://mariadb.com/docs/solutions/htap/) database instance. 

This data can be used within a local MariaDB HTAP instance or one hosted in [MariaDB SkySQL](https://mariadb.com/products/skysql/docs/). 

## Instructions:

Go through the following steps to create the schema, load data, and set up replication for your MariaDB HTAP instance.

1. Clone this repository.

```
$ git clone https://github.com/rhedgpeth/skysql_htap_demo.git
```

2. Execute the following command with your database instance information.

```
$ ./create_and_load.sh <host_address> <port_number> <user> <password>
```

for example

```
./create_and_load.sh sky0001355.mdb0001390.db.skysql.net 5001 DB00009999 *******
```

3.) Execute the following command on your MariaDB SkySQL database instance to set up replication.

```
SELECT SET_HTAP_REPLICATION('flights','travel','travel_history');
```

That's it! The following will be created, loaded, and configured to replicate (travel.flights -> travel_history.flights).

- [travel](schema/idb_schema.sql#L1) (database)
    - [airlines](schema/idb_schema.sql#L5) (InnoDB table): 17 rows
    - [airports](schema/idb_schema.sql#L11) (InnoDB table): 342 rows
    - [flights](schema/idb_schema.sql#L21) (InnoDB table): 0 rows
- [travel_history](schema/cs_schema.sql#L1) (database)
    - [flights](schema/cs_schema.sql#L5) (ColumnStore table): 679996 rows


## More resources

- [Sign up for MariaDB SkySQL](https://mariadb.com/products/skysql/get-started/)
- [MariaDB SkySQL Documentation](https://mariadb.com/products/skysql/docs/)
