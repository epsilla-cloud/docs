# Embeddings

Embeddings/vectors are numerical representations of complex data like text or images in a format that machines can process. Embedding models convert text, images, audios, and videos into vectors of real numbers. This process captures semantic meaning, allowing algorithms to understand content similarity and context. This technique is pivotal in various applications, from Retrieval Augmented Generation (RAG) to recommendation systems to language translation, as it enables computers to 'understand' and work with human language.

<figure><img src="../.gitbook/assets/Screenshot 2023-12-18 at 1.56.44 PM.png" alt=""><figcaption></figcaption></figure>

In embedding models, the mathematical premise is that the closer two vectors are in high-dimensional space, the more semantically similar they are. This characteristic is leveraged in vector databases for semantic similarity search, using algorithms like nearest neighbor search. These algorithms compute the distances between vectors, interpreting smaller distances as higher similarity. This approach enables applications to find closely related items (like texts, images, audios, videos) based on their embedded vector representations, making it possible to conduct searches and analyses based on the meaning and context of the data, rather than just literal matches.

<figure><img src="../.gitbook/assets/Screenshot 2023-12-18 at 3.19.33 PM.png" alt=""><figcaption></figcaption></figure>

## Built-in Embeddings

Starting in v0.3, Epsilla supports automatically embed your documents and questions within the vector database, which significantly simplify the end to end semantic similarity search workflow.

Here is the list of built-in embedding models Epsilla supports:

* BAAI/bge-small-en
* BAAI/bge-small-en-v1.5
* BAAI/bge-small-zh-v1.5
* BAAI/bge-base-en
* BAAI/bge-base-en-v1.5
* sentence-transformers/all-MiniLM-L6-v2

**BAAI/bge-small-en-v1.5** and **sentence-transformers/all-MiniLM-L6-v2** are enabled by default. You can turn on other models via docker run command environment variable EMBEDDING\_MODELS (using comma separated string):

```bash
docker run --pull=always -d -p 8888:8888 -e EMBEDDING_MODELS="BAAI/bge-small-zh-v1.5,BAAI/bge-base-en" epsilla/vectordb
```

When using these built-in embedding models, the embedding are conducted within your local laptop without outbound network. They use CPU first to do the embedding. So make sure you have enough CPU power and memory to handle the models before enabling them.&#x20;

## OpenAI Embedding

Epsilla also wraps **openai/text-embedding-ada-002** embedding out of box. When using OpenAI embedding, make sure provide the **X-OpenAI-API-Key** header when connecting to the vector database:

{% tabs %}
{% tab title="Python" %}
```python
db = vectordb.Client(
    ...
    headers={
        "X-OpenAI-API-Key": <Your OpenAI API key here>
    }
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const db = new epsillajs.EpsillaDB({
    ...
    headers: {
        "X-OpenAI-API-Key": <Your OpenAI API key here>
    }
});
```
{% endtab %}
{% endtabs %}

## Use Embeddings

When creating tables, you can define indices to let Epsilla automatically create embeddings for the STRING fields:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.create_table(
    table_name="MyTable",
    table_fields=[
        {"name": "ID", "dataType": "INT", "primaryKey": True},
        {"name": "Doc", "dataType": "STRING"}
    ],
    indices=[
        {"name": "Index", "field": "Doc", "model": "BAAI/bge-small-en-v1.5"}
    ]
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.createTable('MyTable',
  [
    {"name": "ID", "dataType": "INT", "primaryKey": true},
    {"name": "Doc", "dataType": "STRING"}
  ],
  [
    {"name": "Index", "field": "Doc", "model": "BAAI/bge-small-en-v1.5"}
  ]
);
```
{% endtab %}
{% endtabs %}

Then after inserting records, you can query the table with natural language questions:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.query(
  table_name="MyTable",
  query_text="Where can I find a serene environment, ideal for relaxation and introspection?",
  limit=2
)
print(response)
```

Output

```
{
  'message': 'Query search successfully.',
  'result': [
    {'Doc': 'The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.', 'ID': 3},
    {'Doc': 'High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.', 'ID': 4}
  ],
  'statusCode': 200
}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// search
const query = await db.query(
  'MyTable',
  {
    query: "Where can I find a serene environment, ideal for relaxation and introspection?",
    limit: 2
  }
);
console.log(JSON.stringify(query));
```

Output:

```
{
  "statusCode":200,
  "message":"Query search successfully.",
  "result":[
    {"Doc": "The library was a quiet haven, filled with the scent of old books and the soft rustling of pages.", "ID": 3},
    {"Doc": "High in the mountains, the air was crisp and clear, revealing breathtaking views of the valley below.", "ID": 4}
  ]
}
```
{% endtab %}
{% endtabs %}
