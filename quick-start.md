# 🚀 Quick Start

## 1. Installation

To run a pre-built EpsillaDB image on your machine, make sure Docker is installed on your system.

Download image from [Dockerhub](https://hub.docker.com/r/epsilla/vectordb).

```sh
docker pull epsilla/vectordb
```

Start the docker as the backend service

```sh
docker run --pull=always -d -p 8888:8888 epsilla/vectordb
```

Your EpsillaDB service is up and running. You can use REST API to interact with EpsillaDB, or install a Python/JavaScripy client.

{% tabs %}
{% tab title="Python" %}
```bash
pip3 install --upgrade pyepsilla
```
{% endtab %}

{% tab title="JavaScript" %}
```sh
npm install epsillajs
```
{% endtab %}

{% tab title="Ruby" %}
```sh
gem install epsilla-ruby
```
{% endtab %}
{% endtabs %}

## 2. Connect to EpsillaDB

{% tabs %}
{% tab title="Python" %}
```python
from pyepsilla import vectordb

## connect to vectordb
client = vectordb.Client(
  host='localhost',
  port='8888'
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const epsillajs = require('epsillajs');

// connect to vectordb
const db = new epsillajs.EpsillaDB({
  host: 'localhost',
  port: 9999
});
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "epsilla"

## connect to vectordb
client = Epsilla::Client.new(protocol="http", host="127.0.0.1", port="8888")
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X GET "http://localhost:8888"
```

Response

```sh
Welcome to Epsilla VectorDB.
```
{% endtab %}
{% endtabs %}

Hint: if you are connecting to a secure server, use protocol parameter:

{% tabs %}
{% tab title="Python" %}
```python
client = vectordb.Client(
  protocol='https',
  host=...
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    protocol: 'https',
    host: ...
});
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "epsilla"

## connect to vectordb
client = Epsilla::Client.new(protocol="https", host="127.0.0.1", port="8888")
```
{% endtab %}
{% endtabs %}

## 3. Create or load a database

{% tabs %}
{% tab title="Python" %}
```python
client.load_db(db_name="MyDB", db_path="/tmp/epsilla")
client.use_db(db_name="MyDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.loadDB('/tmp/epsilla', 'MyDB');
db.useDB("MyDB");
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
status_code, response = client.database.load_db(db_name="MyDB", db_path="/tmp/epsilla")
puts status_code, response
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/load' \
    -d '{
        "path": "/tmp/epsilla",
        "name": "MyDB"
    }'
```

Response:

```json
{
    "statusCode": 200,
    "message": "Load/Create MyDB successfully."
}
```
{% endtab %}
{% endtabs %}

## 4. Create a table

{% tabs %}
{% tab title="Python" %}
```python
client.create_table(
  table_name="MyTable",
  table_fields=[
    {"name": "ID", "dataType": "INT", "primaryKey": True},
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
    {"name": "ID", "dataType": "INT", "primaryKey": true},
    {"name": "Doc", "dataType": "STRING"},
    {"name": "Embedding", "dataType": "VECTOR_FLOAT", "dimensions": 4}
  ]
);
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
status_code, response = client.database.create_table(
  table_name="MyTable",
  table_fields=[
  {"name" => "ID", "dataType" => "INT", "primaryKey" => true},
  {"name" => "Doc", "dataType" => "STRING"},
  {"name" => "Embedding", "dataType" => "VECTOR_FLOAT", "dimensions" => 4}
])
puts status_code, response

```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/schema/tables' \
    -d '{
        "name": "MyTable",
        "fields": [
          {
            "name": "ID",
            "dataType": "INT",
            "primaryKey": true
          },
          {
            "name": "Doc",
            "dataType": "STRING"
          },
          {
            "name": "Embedding",
            "dataType": "VECTOR_FLOAT",
            "dimensions": 4
          }
        ]
     }'
```

Response:

```json
{
    "statusCode":200,
    "message":"Create MyTable successfully."
}
```
{% endtab %}
{% endtabs %}

## 5. Insert new records

You can insert multiple records in a batch.

{% tabs %}
{% tab title="Python" %}
```python
client.insert(
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

{% tab title="Ruby" %}
```ruby
status_code, response = client.database.insert(
  table_name="MyTable",
  table_records=[
    {"ID" => 1, "Doc" => "Berlin", "Embedding" => [0.05, 0.61, 0.76, 0.74]},
    {"ID" => 2, "Doc" => "London", "Embedding" => [0.19, 0.81, 0.75, 0.11]},
    {"ID" => 3, "Doc" => "Moscow", "Embedding" => [0.36, 0.55, 0.47, 0.94]},
    {"ID" => 4, "Doc" => "San Francisco", "Embedding" => [0.18, 0.01, 0.85, 0.80]},
    {"ID" => 5, "Doc" => "Shanghai", "Embedding" => [0.24, 0.18, 0.22, 0.44]}  
])
puts status_code, response
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/data/insert' \
    -d '{
        "table": "MyTable",
        "data": [
            {
              "ID": 1,
              "Doc": "Berlin",
              "Embedding": [0.05, 0.61, 0.76, 0.74]
            },
            {
              "ID": 2,
              "Doc": "London",
              "Embedding": [0.19, 0.81, 0.75, 0.11]
            },
            {
              "ID": 3,
              "Doc": "Moscow",
              "Embedding": [0.36, 0.55, 0.47, 0.94]
            },
            {
              "ID": 4,
              "Doc": "San Francisco",
              "Embedding": [0.18, 0.01, 0.85, 0.80]
            },
            {
              "ID": 5,
              "Doc": "Shanghai",
              "Embedding": [0.24, 0.18, 0.22, 0.44]
            }
         ]
     }'          
```

Response:

```json
{
    "statusCode": 200,
    "message": "Insert data to MyTable successfully."
}
```
{% endtab %}
{% endtabs %}

## 6. Search

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = client.query(
  table_name="MyTable",
  query_field="Embedding",
  query_vector=[0.35, 0.55, 0.47, 0.94],
  response_fields=["ID", "Doc", "Embedding"],
  limit=2,
  with_distance=True
)
print(response)
```

Output

```
{'statusCode': 200, 'message': 'Query search successfully.', 'result': [{'ID': 3, 'Doc': 'Moscow', 'Embedding': [0.36, 0.55, 0.47, 0.94]}, {'ID': 1, 'Doc': 'Berlin', 'Embedding': [0.05, 0.61, 0.76, 0.74]}]}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// search
const query = await db.query(
  'MyTable',
  "Embedding", // query field
  [0.35, 0.55, 0.47, 0.94], // query vector
  2 // top K
);
console.log(JSON.stringify(query));
```

Output:

```
{"statusCode":200,"message":"Query search successfully.","result":[{"Doc":"Moscow","Embedding":[0.3600000143051147,0.550000011920929,0.4699999988079071,0.9399999976158142],"ID":3},{"Doc":"Berlin","Embedding":[0.05000000074505806,0.6100000143051147,0.7599999904632568,0.7400000095367432],"ID":1}]}
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
status_code, response = client.database.query(
  table_name="MyTable",
  query_field="Embedding",
  query_vector=[0.35, 0.55, 0.47, 0.94],
  response_fields=["Doc"],
  limit=2,
  with_distance=true)
puts status_code, response
```

Output

```
{'statusCode': 200, 'message': 'Query search successfully.', 'result': [{'ID': 3, 'Doc': 'Moscow', 'Embedding': [0.36, 0.55, 0.47, 0.94]}, {'ID': 1, 'Doc': 'Berlin', 'Embedding': [0.05, 0.61, 0.76, 0.74]}]}
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/data/query' \
    -d '{
        "table": "MyTable",
        "queryField": "Embedding",
        "queryVector": [0.35, 0.55, 0.47, 0.94],
        "limit": 2,
        "withDistance": true
     }'        
```

Response:

```json
{
    "statusCode": 200,
    "message": "Query search successfully.",
    "result": [
        {
            "ID": 3,
            "Doc": "Moscow",
            "Embedding": [0.36, 0.55, 0.47, 0.94]
        },
        {
            "ID": 1,
            "Doc": "Berlin",
            "Embedding": [0.05, 0.61, 0.76, 0.74]
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## 7. Drop a table

Drop a table will remove the

{% tabs %}
{% tab title="Python" %}
```python
client.drop_table("MyTable")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.dropTable('MyTable');
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
client.database.drop_table("MyTable")
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X DELETE 'http://localhost:8888/api/MyDB/schema/tables/MyTable'      
```

Response:

```json
{
    "statusCode": 200,
    "message": "Drop MyTable from MyDB successfully."
}
```
{% endtab %}
{% endtabs %}

## 5. Unload a database

Offload a database that is not in use to release memory (the database files are still on disk).

{% tabs %}
{% tab title="Python" %}
```python
client.unload_db("MyDB")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.unloadDB('MyDB');
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
client.database.unload_db("MyDB")
```
{% endtab %}

{% tab title="cURL" %}
```sh
curl -X POST 'http://localhost:8888/api/MyDB/unload'      
```

Response:

```json
{
    "statusCode": 200,
    "message": "Unload MyDB successfully."
}
```
{% endtab %}
{% endtabs %}

## Next steps[​](https://docs.trychroma.com/getting-started#-next-steps) <a href="#next-steps" id="next-steps"></a>

EpsillaDB is designed to be simple enough to get started. Refer to [API Reference](api-reference.md) for more flexibility and options on each API.

We are tirelessly working to enhance EpsillaDB with more features. Please consult our [Roadmap](roadmap.md) to glimpse into the future developments.
