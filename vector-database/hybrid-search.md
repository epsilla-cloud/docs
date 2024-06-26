# Hybrid Search

### What is Hybrid Search

Hybrid search is an advanced retrieval technique that enhances search accuracy and relevance by integrating multiple search algorithms. Typically it combines traditional **keyword-based** **search** with the contextual understanding offered by **vector semantic search**.&#x20;

Traditionally, search engines relied on keyword-based algorithms, excelling in exact keyword matching but faltering with synonyms and typos, thereby missing contextually relevant results. The advent of machine learning introduced vector or semantic search, utilizing vector embeddings to grasp and search data semantically, supporting multi-lingual and multi-modal queries while being robust to typos. However, it sometimes overlooks crucial keywords and is dependent on the quality of embeddings, sensitive to out-of-domain terms.&#x20;

Hybrid search leverages the strengths of both, employing sparse vectors (generated by algorithms like BM25 and SPLADE) for keyword precision and dense vectors (from models like  [OpenAI/text-embedding-ada-002](https://platform.openai.com/docs/guides/embeddings/second-generation-models), [sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)) for contextual understanding. For example, when someone searches "How to catch a Rainbow Trout," hybrid search leverages dense vectors to interpret "catch" within the context of fishing, so it doesn't confuse with semantic meaning of "catching a basketball" or so. Simultaneously, it employs sparse vectors to ensure terms like "Rainbow Trout" are matched with pinpoint accuracy. This approach not only bridges the gap between keyword specificity and semantic context but also ensures a nuanced search experience that accurately interprets complex queries.

### Hybrid Search Architecture

Here is a hybrid search architecture. When the user query comes, it will trigger multiple retrievers to retrieve the top K documents based on their dense vector embeddings, sparse vector embeddings, (and potentially other indices) concurrently. Each retriever gives back a list of documents as candidate results. Then, the documents go through a reranker component to calculate the final rank of all documents from all retrievers, and give the final retrieval result.

<figure><img src="../.gitbook/assets/Screenshot 2024-02-19 at 6.27.45 PM.png" alt=""><figcaption><p>Hybrid Search Architecture</p></figcaption></figure>

### Epsilla Hybrid Search API

Here is a hybrid search example:

{% tabs %}
{% tab title="Python" %}
```python
search_engine = db.as_search_engine( 
).add_retriever(
     table_name="MyTable",
     query_index="DenseIndex",
     limit=4,
).add_retriever(
     table_name="MyTable",
     query_field="SparseIndex",
     query_vector={
        "indices": [32, 103, 2345, 10384],
        "values": [0.074163, 0.238575, 0.141831, 0.117338]
     },
     limit=2,
).set_reranker(
     type="rrf"
)

search_result = search_engine.search(
    "Where can I find a serene environment, ideal for relaxation and introspection?"
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const searchEngine = db
    .asSearchEngine()
    .addRetriever({
        table: 'MyTable',
        indexName: 'MyIndex1',
        limit: 4,
    })
    .addRetriever({
        table: 'MyTable',
        queryField: 'SparseIndex',
        queryVector: {
            indices: [32, 103, 2345, 10384],
            values: [0.074163, 0.238575, 0.141831, 0.117338]
        },
        limit: 2,
    })
    .setReranker('rrf');

const searchResults = await searchEngine.search(
    'Where can I find a serene environment, ideal for relaxation and introspection?'
);
```
{% endtab %}
{% endtabs %}

Now let's breakdown hybrid search API step by step.

#### Prerequisite:

Assume you have already [connected to a vector database](connect-to-a-database.md).

{% tabs %}
{% tab title="Python" %}
```python
# Open source
db = vectordb.Client(...)
db.use_db(db_name="...")

# Epsilla cloud
db = cloud.Client(...).vectordb(...)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
// Open source
const db = new epsillajs.EpsillaDB(...);
db.useDB(...);

// Epsilla cloud
const cloud = new epsillajs.EpsillaCloud(...);
const db = new epsillajs.VectorDB(...); 
await db.connect();
```
{% endtab %}
{% endtabs %}

#### Step 1. Convert the vector database as a search engine

{% tabs %}
{% tab title="Python" %}
```python
search_engine = db.as_search_engine()
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const searchEngine = db.asSearchEngine()
```
{% endtab %}
{% endtabs %}

#### Step 2. Add retrievers

You can add one or many retrievers to the search engine. A retriever can retrieve documents on an index, or an embedding field (either dense or sparse embedding).

Add retriever on an index:

{% tabs %}
{% tab title="Python" %}
```python
search_engine.add_retriever(
  primary_key_field="ID",                # (Optional) Which field to use as document's ID. Default value is "ID"
  table_name="MyTable",                  # The name of the table to retrieve against.
  query_index="MyIndex",                 # The index name to retrieve against.
  limit=2,                               # The top K result to return.
  response_fields=["Doc"],               # (Optional) which fields to be included in
                                         # the response. If not provided, will include
                                         # all fields in the table.
  filter="ID < 6 AND Doc <> 'London'",   # (Optional) a boolean expression for filtering
                                         # out the results.
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
searchEngine.addRetriever(
  'MyTable',                                 // The name of the table to retrieve against.
  {
    primaryKeyField: 'ID',                   // (Optional) Which field to use as document's ID. Default value is 'ID'
    queryIndex: 'MyIndex',                   // The index name to retrieve against.
    limit: 2,                                // The top K result to return.
    response: ["Doc"],                       // (Optional) which fields to be included in
                                             // the response. If not provided, will include
                                             // all fields in the table.
    filter: 'ID < 6 AND Doc <> \'London\'',  // (Optional) filter: a boolean expression for filtering
                                             // out the results.
  }
);
```
{% endtab %}
{% endtabs %}

Add retriever on an embedding field:

{% tabs %}
{% tab title="Python" %}
```python
search_engine.add_retriever(
  primary_key_field="ID",                # (Optional) Which field to use as document's ID. Default value is "ID"
  table_name="MyTable",                  # The name of the table to retrieve against.
  query_field="SparseIndex",             # The embedding field
  query_vector={                         # The vector embedding of the query (either dense or sparse)
    "indices": [32, 103, 2345, 10384],
    "values": [0.074163, 0.238575, 0.141831, 0.117338]
  },
  limit=2,                               # The top K result to return.
  response_fields=["Doc"],               # (Optional) which fields to be included in
                                         # the response. If not provided, will include
                                         # all fields in the table.
  filter="ID < 6 AND Doc <> 'London'",   # (Optional) a boolean expression for filtering
                                         # out the results.
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
searchEngine.addRetriever(
  'MyTable',                                 // The name of the table to retrieve against.
  {
    primaryKeyField: 'ID',                   // (Optional) Which field to use as document's ID. Default value is 'ID'
    queryField: 'SparseIndex',               // The embedding field
    queryVector: {                           // The vector embedding of the query (either dense or sparse)
      indices: [32, 103, 2345, 10384],
      values: [0.074163, 0.238575, 0.141831, 0.117338]
    },
    limit: 2,                                // The top K result to return.
    response: ["Doc"],                       // (Optional) which fields to be included in
                                             // the response. If not provided, will include
                                             // all fields in the table.
    filter: 'ID < 6 AND Doc <> \'London\'',  // (Optional) filter: a boolean expression for filtering
                                             // out the results.
  }
);
```
{% endtab %}
{% endtabs %}

If you only add one retriever, the search degrades to a simple query.

**Step 3. Set reranker**

If more than one retriever is added to the search engine, you must set a reranker. Here is a simplest example for adding a reciprocal rank fusion (rrf) reranker. Go to the [reranker](hybrid-search.md#reranker) section to learn more.

{% tabs %}
{% tab title="Python" %}
```python
search_engine.set_reranker(type="rrf")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
searchEngine.setReranker('rrf');
```
{% endtab %}
{% endtabs %}

#### Step 4. Search

Now the search engine is ready to use. Call the search API to get the hybrid search results.

{% tabs %}
{% tab title="Python" %}
```python
search_result = search_engine.search(
    "Where can I find a serene environment, ideal for relaxation and introspection?"
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const searchResults = await searchEngine.search(
    'Where can I find a serene environment, ideal for relaxation and introspection?'
);
```
{% endtab %}
{% endtabs %}

### Reranker

Epsilla supports a growing number of rerankers:

#### Reciprocal Rank Fusion (RRF)

RRF uses the following formula to determine the score for ranking each document:

```python
score = 0.0
for i, retriever in retrievers:
    if doc in retriever.results:
        score += weights[i] / ( k + rank( retriever.results, doc ) )
return score

# k is a ranking constant, default to 50
# i is the index of the retriever among all retrievers
# retriever.results is the list of documents retrieved from the retriever
# doc is a document we calculate the final ranking
# weights[i] is the weight we give to the i-th retriever.
# rank( retriever.results, doc ) is doc's rank within retriever.results starting from 1
```

You can see the higher the rank of a document in a retriever, the higher the score. The document that ranks ahead in more retrievers will be ranked ahead in the final reranking result.

Here is the full API for using Reciprocal Rank Fusion reranker:

{% tabs %}
{% tab title="Python" %}
<pre class="language-python"><code class="lang-python">search_engine.set_reranker(
    type="rrf",          # or "reciprocal_rank_fusion"
    weights=[0.3, 0.7],  # (Optional) give a weight for different retrivers, will use [1, 1, ...] if not provided
<strong>    k=50,                # (Optional) ranking constant, default to 50 if not provided.
</strong><strong>    limit=3,             # (Optional) limit the top K results after reranking. If not provided, all documents from all retrievers will be returned
</strong>)
</code></pre>
{% endtab %}

{% tab title="JavaScript" %}
```javascript
searchEngine.setReranker(
    'rrf',                    // or 'reciprocal_rank_fusion'
    {
        weights: [0.3, 0.7],  // (Optional) give a weight for different retrivers, will use [1, 1, ...] if not provided
        k: 50,                // (Optional) ranking constant, default to 50 if not provided.
        limit: 3,             // (Optional) limit the top K results after reranking. If not provided, all documents from all retrievers will be returned
    }
);
```
{% endtab %}
{% endtabs %}

#### Relative Score Fusion (RSF)

RSF normalizes and combines scores from multiple retrievers to rank each document. The process involves:

1. Normalizing distances from each source to a score between 0 and 1, where 0 indicates the furthest and 1 the closest to the query among the retrieval results of one retriever.
2. Aggregating these normalized scores for each document across all sources.
3. Ranking documents based on their aggregated scores, with higher scores indicating higher relevance.

Here is the full API for using Relative Score Fusion reranker:

{% tabs %}
{% tab title="Python" %}
```python
search_engine.set_reranker(
    type="rsf",          # or "relative_score_fusion"
    limit=3,             # (Optional) limit the top K results after reranking. If not provided, all documents from all retrievers will be returned
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
searchEngine.setReranker(
    'rsf',                    // or 'relative_score_fusion'
    {
        limit: 3,             // (Optional) limit the top K results after reranking. If not provided, all documents from all retrievers will be returned
    }
);
```
{% endtab %}
{% endtabs %}

#### Distribution-Based Score Fusion (DBSF)

DBSF is a more advanced reranking algorithm than RSF, which takes the embedding distribution of different embedding models, and normalize within the 3 sigma range from median of the embedding distance. [Learn more here](https://medium.com/plain-simple-software/distribution-based-score-fusion-dbsf-a-new-approach-to-vector-search-ranking-f87c37488b18). \
To use DBSF, you will need to provide a scale range for each embedding or index field. [Talk to us](https://epsilla-ai.larksuite.com/scheduler/a80f6a3202d4c328) if you need help to setup the parameters.

Here is the full API for using Distribution-Based Score Fusion reranker:

{% tabs %}
{% tab title="Python" %}
```python
search_engine.set_reranker(
    type="dbsf",         # or "distribution_based_score_fusion"
    scale_ranges=[       # Provide the scale range for each retriever based on the embedding model used
        [0.4, 0.8],
        [0.18, 0.3]
    ],
    limit=3,             # (Optional) limit the top K results after reranking. If not provided, all documents from all retrievers will be returned
)
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
searchEngine.setReranker(
    'dbsf',                  // or 'distribution_based_score_fusion'
    {
        scaleRanges: [       // Provide the scale range for each retriever based on the embedding model used
            [0.4, 0.8],
            [0.18, 0.3]
        ],
        limit: 3,            // (Optional) limit the top K results after reranking. If not provided, all documents from all retrievers will be returned
    }
);
```
{% endtab %}
{% endtabs %}
