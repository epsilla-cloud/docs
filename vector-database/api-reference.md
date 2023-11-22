# Drop a table

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
