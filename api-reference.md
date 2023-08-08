# ⚙ API Reference

## Initialize Client

{% tabs %}
{% tab title="Python" %}
```python
### client connect to localhost
from pyepsilla import vectordb
client = vectordb.Client()


### client connect to remote server
from pyepsilla import vectordb
client = vectordb.Client(
    protocol='http',      # http or https. Default is http
    host='3.100.100.100', # The host machine for the vector db. Default localhost
    port='8888'           # The port for the vector db, default 8888
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// client connect to localhost
const epsillajs = require('epsillajs');
const db = new epsillajs.EpsillaDB();

// client connect to remote server
const epsillajs = require('epsillajs');
const db = new epsillajs.EpsillaDB({
    protocol: 'http',      // http or https. Default is http
    host: '3.100.100.100', // The host machine for the vector db. Default localhost
    port: '8888'           // The port for the vector db, default 8888
});
```
{% endtab %}
{% endtabs %}

## Methods related to database

In Epsilla, the data are organized as databases. A database is consisted of multiple tables.

### Load database

Use the command to load a database into memory. Epsilla can hold multiple databases in memory at the same time.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = client.load_db(
    db_name="myDB",         # The name of the DB. Can give any valid
                            # name when loading a DB from disk.
    db_path="/tmp/epsilla", # The path on the disk where the DB is persisted. 
                            # If the path doesn't exist, will create
                            # a new DB at this path.
    vector_scale=1000000,   # (Optional) the limit of the number of records in
                            # the table. Can provide any positive number at
                            # load_db time. If not specified, the default value
                            # is 150000.
    wal_enabled=True        # (Optional) Enable write ahead log or not. Default 
                            # is True. For high throughput low consistency case,
                            # can disable it to save disk IO.
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const load = await db.loadDB(
    "/tmp/epsilla", // The path on the disk where the DB is persisted. 
                    // If the path doesn't exist, will create
                    // a new DB at this path.
    "MyDB",         // The name of the DB. Can give any valid
                    // name when loading a DB from disk.
    1000000,        // (Optional) the limit of the number of records in
                    // the table. Can provide any positive number at
                    // loadDB time. If not specified, the default value
                    // is 150000.
    true            // (Optional) Enable write ahead log or not. Default 
                    // is True. For high throughput low consistency case,
                    // can disable it to save disk IO.
);
```
{% endtab %}
{% endtabs %}

### Use database

You can use the command to switch between multiple databases that are already loaded in memory. Then the following interactions will be towards this database.

{% tabs %}
{% tab title="Python" %}
```python
client.use_db(db_name="myDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
db.useDB("MyDB");
```
{% endtab %}
{% endtabs %}

### Unload database

You can use this command to unload a database from memory. The database files are still retained on disk.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = client.unload_db(db_name="myDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.unloadDB('MyDB');
```
{% endtab %}
{% endtabs %}

## Methods related to Table

In Epsilla, you can have multiple tables in a database. A table has its name, and multiple fields. Each field has its name, data type, and specific configurations.

### Create a new table

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = client.create_table(
    table_name="MyTable",
    table_fields=[
        {"name": "ID", "dataType": "INT"},
        {"name": "Doc", "dataType": "STRING"},
        {"name": "Embedding", "dataType": "VECTOR_FLOAT", "dimensions": 4}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable('MyTable',
  [
    {"name": "ID", "dataType": "INT"},
    {"name": "Doc", "dataType": "STRING"},
    {"name": "Embedding", "dataType": "VECTOR_FLOAT", "dimensions": 4}
  ]
);
```
{% endtab %}
{% endtabs %}

Here are supported data types:

```
TINYINT      # An int with value range [-256, 255]
SMALLINT     # An int with value range [-65536, 65535]
INT          # An int with value range [-2147483648, 2147483647]
BIGINT       # An int with value range [-9223372036854775808, 9223372036854775807]
FLOAT        # A float field
DOUBLE       # A double field
STRING       # A string field
BOOL         # A boolean field
VECTOR_FLOAT # A vector of float field, dimension must be provided
```

Epsilla supports defining multiple embedding fields in one table. This is very convenient for you to manage multiple embeddings (could be embedded from different models) for the same documents.&#x20;

### Drop a table from a database

Note: when dropping a table, the data on disk will also be removed.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = client.drop_table(table_name="MyTable")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.dropTable('MyTable');
```
{% endtab %}
{% endtabs %}

## Methods related to records

Each table can hold multiple records.&#x20;

### Insert records

Make sure the records comply with the defined table schema.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = client.insert(
  table_name="MyTable",
  records=[
    {"ID": 1, "Doc": "Berlin", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "London", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "Moscow", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "San Francisco", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "Shanghai", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.insert('MyTable',
  [
    {"ID": 1, "Doc": "Berlin", "Embedding": [0.05, 0.61, 0.76, 0.74]},
    {"ID": 2, "Doc": "London", "Embedding": [0.19, 0.81, 0.75, 0.11]},
    {"ID": 3, "Doc": "Moscow", "Embedding": [0.36, 0.55, 0.47, 0.94]},
    {"ID": 4, "Doc": "San Francisco", "Embedding": [0.18, 0.01, 0.85, 0.80]},
    {"ID": 5, "Doc": "Shanghai", "Embedding": [0.24, 0.18, 0.22, 0.44]}
  ]
);
```
{% endtab %}
{% endtabs %}

### Search the top K semantically similar records

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = client.query(
  table_name="MyTable",                  # The name of the table to query against.
  query_field="Embedding",               # The embedding field name to query against.
  query_vector=[0.35, 0.55, 0.47, 0.94], # The embedded vector from the question.
  limit=2,                               # The top K result to return.
  response_fields=["Doc"],               # (Optional) which fields to be included in
                                         # the response. If not provided, will include
                                         # all fields in the table.
  with_distance=True                     # (Optional) include the distance or not in
                                         # the response. Default is False. When given
                                         # as True, each matched record will have a
                                         # @distance field returned.
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const query = await db.query(
  'MyTable',                  // The name of the table to query against.
  'Embedding',                // The embedding field name to query against.
  [0.35, 0.55, 0.47, 0.94],   // The embedded vector from the question.
  2,                          // The top K result to return.
  ["Doc"],                    // (Optional) which fields to be included in
                              // the response. If not provided, will include
                              // all fields in the table.
  true                        // (Optional) include the distance or not in
                              // the response. Default is False. When given
                              // as true, each matched record will have a
                              // @distance field returned.
)
```
{% endtab %}
{% endtabs %}
