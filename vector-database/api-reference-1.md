# Delete records

Delete records with primary keys:

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.delete(
  table_name="MyTable",        # The name of the table to delete records against.
  primary_keys=[1, 2, 5]       # The primary keys of the records to be deleted.
)
print(response)
```

Response example:

```
{'statusCode': 200, 'message': 'successfully deleted 3 records.'}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const query = await db.delete(
  'MyTable',                  // The name of the table to delete records against.
  {
    primaryKeys: [1, 2, 5]    // The primary keys of the records to be deleted.
  }
);
console.log(JSON.stringify(query, undefined, 2));
```

Response example:

```
{
  "statusCode": 200,
  "message": "successfully deleted 3 records."
}
```
{% endtab %}
{% endtabs %}

