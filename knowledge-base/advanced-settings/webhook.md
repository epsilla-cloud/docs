# Webhook

The Webhook is used to receive updates on the status of knowledge base data processing. It provides an effective way to integrate with an enterprise's in-house data processing pipeline, allowing for real-time monitoring and automation of workflows based on processing events.

Provide an endpoint where Epsilla should post status updates:

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 6.24.55 PM.png" alt="" width="563"><figcaption></figcaption></figure>

When the data processing starts, we will POST the following payload to your webhook endpoint:

```json
{
    "datasourceid": <DataSourceID>,
    "timestamp": 1716414820.557603,
    "detail": {
        "status": "processing"
    }
}
```

When the data processing finishes, we will POST the following payload to your webhook endpoint:

```json
{
    "datasourceid": <DataSourceID>,
    "timestamp": 1716414812.8154922,
    "detail": {
        "status": "ready"
    }
}
```

The DataSourceID is an identifier for your knowledge base's data source. You can get the knowledge base's data source ID from the URL (the last parameter of the link):

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 6.39.34 PM.png" alt=""><figcaption></figcaption></figure>
