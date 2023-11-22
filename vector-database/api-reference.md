# Drop a table

## Drop a table from a database using Epsilla Docker&#x20;

Note: when dropping a table, the data on disk will also be removed.

{% tabs %}
{% tab title="Python" %}
```python
status_code, response = db.drop_table(table_name="MyTable")
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
await db.dropTable('MyTable');
```
{% endtab %}
{% endtabs %}

## Drop a table on Epsilla Cloud

For now, you can drop vector tables via Cloud GUI.

<figure><img src="../.gitbook/assets/Screenshot 2023-11-22 at 12.27.54 AM (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
We will support dropping tables via Python/JavaScript client in the near future.
{% endhint %}
