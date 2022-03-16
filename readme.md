## Title
Proof of concept of strange H2 behavior during create functional index (PostgreSQL-oriented context).

## Description
When trying to create a functional index using liquibase migration (H2 with PostgreSQL-oriented context), an ambiguous error occurs. 
Judging by the reports in the log, liquibase creates an incorrect index creation script.

The problem was found in earlier versions, but is confirmed in more than fresh (tested on `3.10.3` and `4.8.10` versions).
The test script is located in the `create_test_table.xml`. Creates a table and tries to create a functional index.

Error log message: 
```
Syntax error in SQL statement "CREATE INDEX TEST_TABLE_ID_IDX ON TEST_TABLE(([*]DATE_TRUNC('day', CREATE_DATE)))"; expected "identifier"; 
SQL statement: CREATE INDEX test_table_id_idx ON test_table((date_trunc('day', create_date))) [42001-200]
```

For checking execute `mvn compile`.
