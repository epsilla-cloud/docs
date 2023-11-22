---
description: >-
  In Epsilla, the data are organized as databases. A database is consisted of
  multiple tables.
---

# Connect to a database

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
