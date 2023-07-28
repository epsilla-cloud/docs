# ⚙ API Reference

## Initialize client - Python

### client for localhost

```python
from pyepsilla import vectordb
client = vectordb.Client()
```
### client for remote server
```python
from pyepsilla import vectordb
client = vectordb.Client(host='3.100.100.100', port='8888', db_name='default')
```


## Methods on Client

### Methods related to database

#### load and use database with path config
```python
status_code, response = client.load_db(db_name="myDB", db_path="/tmp/epsilla")
client.use_db(db_name="myDB")
```

#### unload database
```python
status_code, response = client.unload_db(db_name="myDB")
```
#### drop database
```python
status_code, response = client.drop_db(db_name="myDB")
```


### Methods related to Table

#### define table field schema
```python
dimensions = 4
id_field = {"name": "ID", "dataType": "INT", "primaryKey": True}
doc_field = {"name": "Doc", "dataType": "STRING"}
vec_field = {"name": "Embedding", "dataType": "VECTOR_FLOAT", "dimensions": dimensions}

fields = [id_field, doc_field, vec_field]
```

#### create one table with schema definition in specific database
```python

client.use_db(db_name="myDB")
status_code, response = client.create_table(table_name="MyTable", table_fields=fields)
```

#### drop specific table
```python
status_code, response = client.drop_table(table_name="MyTable")
```

#### define new records following field schema
```python
Ids = [ i for i in range(5)]
Docs = ["Berlin", "London", "Moscow", "San Francisco", "Shanghai"]
Embedding =[[0.05, 0.61, 0.76, 0.74],
            [0.19, 0.81, 0.75, 0.11],
            [0.36, 0.55, 0.47, 0.94],
            [0.18, 0.01, 0.85, 0.80],
            [0.24, 0.18, 0.22, 0.44]
           ]
```

#### insert new records into specific table
```python
records_data = [ {"ID": i, "Doc": Docs[i], "Embedding": Embedding[i]} for i in range(len(Ids))]
status_code, response = c.insert(table_name="MyTable", records=records_data)
```

### Methods related to vector search in table

#### define query/response parameters and do vector search
```python
query_field = "Embedding"
response_fields = ["Doc"]

query_vector = [0.24, 0.18, 0.22, 0.44]
limit = 2

status_code, response = c.query(table_name="MyTable", query_field=query_field, query_vector=query_vector, response_fields=response_fields, limit=limit)
print("status_code", status_code, "response", response)
```








