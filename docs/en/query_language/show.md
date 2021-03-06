# SHOW Queries

## SHOW CREATE TABLE

```sql
SHOW CREATE [TEMPORARY] [TABLE|DICTIONARY] [db.]table [INTO OUTFILE filename] [FORMAT format]
```

Returns a single `String`-type 'statement' column, which contains a single value – the `CREATE` query used for creating the specified object.

## SHOW DATABASES {#show-databases}

```sql
SHOW DATABASES [INTO OUTFILE filename] [FORMAT format]
```

Prints a list of all databases.
This query is identical to `SELECT name FROM system.databases [INTO OUTFILE filename] [FORMAT format]`.

## SHOW PROCESSLIST

```sql
SHOW PROCESSLIST [INTO OUTFILE filename] [FORMAT format]
```

Outputs the content of the [system.processes](../operations/system_tables.md#system_tables-processes) table, that contains a list of queries that is being processed at the moment, excepting `SHOW PROCESSLIST` queries.

The `SELECT * FROM system.processes` query returns data about all the current queries.

Tip (execute in the console):

```bash
$ watch -n1 "clickhouse-client --query='SHOW PROCESSLIST'"
```

## SHOW TABLES

Displays a list of tables.

```sql
SHOW [TEMPORARY] TABLES [FROM <db>] [LIKE '<pattern>'] [LIMIT <N>] [INTO OUTFILE <filename>] [FORMAT <format>]
```

If the `FROM` clause is not specified, the query returns the list of tables from the current database.

You can get the same results as the `SHOW TABLES` query in the following way:

```sql
SELECT name FROM system.tables WHERE database = <db> [AND name LIKE <pattern>] [LIMIT <N>] [INTO OUTFILE <filename>] [FORMAT <format>]
```

**Example**

The following query selects the first two rows from the list of tables in the `system` database, whose names contain `co`.

```sql
SHOW TABLES FROM system LIKE '%co%' LIMIT 2
```
```text
┌─name───────────────────────────┐
│ aggregate_function_combinators │
│ collations                     │
└────────────────────────────────┘
```

## SHOW DICTIONARIES

Displays a list of [external dictionaries](dicts/external_dicts.md).

```sql
SHOW DICTIONARIES [FROM <db>] [LIKE '<pattern>'] [LIMIT <N>] [INTO OUTFILE <filename>] [FORMAT <format>]
```

If the `FROM` clause is not specified, the query returns the list of dictionaries from the current database.

You can get the same results as the `SHOW DICTIONARIES` query in the following way:

```sql
SELECT name FROM system.dictionaries WHERE database = <db> [AND name LIKE <pattern>] [LIMIT <N>] [INTO OUTFILE <filename>] [FORMAT <format>]
```

**Example**

The following query selects the first two rows from the list of tables in the `system` database, whose names contain `co`.

```sql
SHOW DICTIONARIES FROM db LIKE '%reg%' LIMIT 2
```
```text
┌─name─────────┐
│ regions      │
│ region_names │
└──────────────┘
```
