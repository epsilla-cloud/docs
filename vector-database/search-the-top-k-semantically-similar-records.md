# Search the top K semantically similar records

### Search the top K semantically similar records

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.query(
  table_name="MyTable",                  # The name of the table to query against.
  query_field="Embedding",               # The embedding field name to query against.
  query_vector=[0.35, 0.55, 0.47, 0.94], # The embedded vector from the question.
  limit=2,                               # The top K result to return.
  response_fields=["Doc"],               # (Optional) which fields to be included in
                                         # the response. If not provided, will include
                                         # all fields in the table.
  filter="ID < 6 AND Doc <> 'London'",   # (Optional) a boolean expression for filtering
                                         # out the results.
  with_distance=True                     # (Optional) include the distance or not in
                                         # the response. Default is False. When given
                                         # as True, each matched record will have a
                                         # @distance field returned.
)
print(response)
```

Response example:

```
{'statusCode': 200, 'message': 'Query search successfully.', 'result': [{'@distance': 0.0001000004049274139, 'Doc': 'Moscow'}, {'@distance': 0.2176999747753143, 'Doc': 'Berlin'}]}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const query = await db.query(
  'MyTable',                                 // The name of the table to query against.
  {
    queryField: 'Embedding',                 // The embedding field name to query against.
    queryVector: [0.35, 0.55, 0.47, 0.94],   // The embedded vector from the question.
    limit: 2,                                // The top K result to return.
    response: ["Doc"],                       // (Optional) which fields to be included in
                                             // the response. If not provided, will include
                                             // all fields in the table.
    filter: 'ID < 6 AND Doc <> \'London\'',  // (Optional) filter: a boolean expression for filtering
                                             // out the results.
    withDistance: true                       // (Optional) include the distance or not in
                                             // the response. Default is False. When given
                                             // as true, each matched record will have a
                                             // @distance field returned.
  }
);
console.log(JSON.stringify(query, undefined, 2));
```

Response example:

```
{
  "statusCode": 200,
  "message": "Query search successfully.",
  "result": [
    {
      "@distance": 0.0001000004049274139,
      "Doc": "Moscow"
    },
    {
      "@distance": 0.2176999747753143,
      "Doc": "Berlin"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

#### Filter Expression

Epsilla supports filter expression in search that is compatible with SQL. The following operators are supported:

| Operator | Description                                           |
| -------- | ----------------------------------------------------- |
| +        | Add                                                   |
| -        | Subtract                                              |
| \*       | Multiply                                              |
| /        | Divide                                                |
| %        | Modulo                                                |
| =        | Equal to                                              |
| >        | Greater than                                          |
| <        | Less than                                             |
| >=       | Greater than or equal to                              |
| <=       | Less than or equal to                                 |
| <>       | Not equal to                                          |
| AND      | TRUE if all the conditions separated by AND is TRUE   |
| NOT      | TRUE if the condition afterward is NOT TRUE           |
| OR       | TRUE if any of the conditions separated by OR is TRUE |

A string literal needs to be surrounded by single quotes.&#x20;

Refer to a field of the record directly by the field name.

Providing an empty filter is same as not providing the filter at all (all records will pass the evaluation).
