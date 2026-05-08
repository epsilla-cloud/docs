# Programmatically Manage Knowledge Bases

In this section, we introduce the REST APIs for managing knowledge bases. This allows developers to efficiently interact with and update the knowledge base using automation and code.

### Get Knowledge Base Data Source Config Details

**Request:**

```sh
curl -X GET https://etl.epsilla.com/api/v1/datasources/<project_id>/pipeline/<datasource_id> \
     -H "X-API-Key: <Project-API-Key>" 
```

The project\_id and datasource\_id are identifiers for your project and your knowledge base's data source. You can obtain the project ID and data source ID from the URL:

<figure><img src="../.gitbook/assets/Screenshot 2024-10-07 at 1.29.01 AM.png" alt=""><figcaption></figcaption></figure>

You can find how to get the Project API Key in [Project Management](../project-management.md).

**Response:**

```json
{
    "statusCode": 200,
    "message": "Get pipeline successfully.",
    "result": {
        "name": "<knowledge_base_name>",
        "resource_id": "<datasource_id>",
        "updated_at": 1721318300666,
        "created_at": 1721318285687,
        "status": "Active",
        "sync_status": "synchronized", 
        "last_synced": 1721318341060,
        "creator_user_id": "user1@example.com",
        "configs": {                 // Knowledge base data source configs
            "source_type": "file",
            "source_config": {},
            "auto_sync": false,
            "sync_schedule": "",
            "loader_type": "auto",   // Loading config
            "chunk_config": {        // Chunking config
                "type": "sentence",
                "chunk_overlap": 192,
                "chunk_size": 1024
            },
            "embed_model": "openai/text-embedding-3-large",  // Embedding config
            "web_hook": "",
            "meta_file_pattern": "",
            "meta_fields": []
        },
        "files_status": [    // Data processing status
            {
                "entity_type": "FileSyncStatus",
                "sync_status": "synchronized",
                "last_synced": 1721318325641,
                "name": "<FileName>"
            }
        ]
    }
}
```

### Create a New S3 Knowledge Base (And Trigger Initial Loading)

**Request**

```bash
curl -X POST https://etl.epsilla.com/api/v1/datasources/<project_id>/create \
     -H "X-API-Key: <Project-API-Key>" \
     -d {
       "name": "<knowledge_base_name>",
       "source_type":"s3",
       "source_config":{"aws_key_id":"<secret_key>","aws_access_key":"<access_key>","bucket":"<bucket_name>","prefix":"<object_prefix>"},
       "loader_type":"auto",
       "chunk_config":{"type":"sentence","chunk_size":1024,"chunk_overlap":192},
       "embed_model":"openai/text-embedding-3-large",
       "auto_sync": false,
       "web_hook": "<The full URL that will receive the loading job status update>"
     }
```

**Response:**

```json
{
    "statusCode": 200,
    "message": "Success to create and execute datasource <datasource_id> for project <project_id>",
    "result": {
        "project_id": <project_id>,
        "datasource": <datasource_id>, // Please keep this ID for your record.
        "status": "Created"
    }
}
```

### Update Knowledge Base Config

**Request**

```bash
curl -X PUT https://etl.epsilla.com/api/v1/datasources/<project_id>/pipeline/update/<datasource_id> \
     -H "X-API-Key: <Project-API-Key>" \
     -d '{"auto_sync": true, "sync_schedule": "15min"}' # Only provide the entries that need to be updated
```

**Response:**

```json
{
    "statusCode": 200,
    "message": "Update pipeline successfully.",
    "result": {
        ...   // The knowledge base config
    }
}
```

### Reprocess Data In Knowledge Base

**Request**

```bash
curl -X POST https://etl.epsilla.com/api/v1/datasources/<project_id>/pipeline/<datasource_id> \
     -H "X-API-Key: <Project-API-Key>"
```

**Response:**

```json
{
    "statusCode": 200,
    "message": "Start to execute data pipeline successfully.",
    "result": {
        "task_id": "<data_processing_task_id>",
        "pipeline_id": "<datasource_id>"
    }
}
```

### Check Knowledge Base Data Processing Progress

**Request:**

```sh
curl -X GET https://etl.epsilla.com/api/v1/datasources/<project_id>/pipeline/<datasource_id>/status \
     -H "X-API-Key: <Project-API-Key>" 
```

**Response:**

<pre class="language-json"><code class="lang-json">// In process
{
    "statusCode": 200,
    "message": "Pipeline still have 1  un-successful sub_tasks.",
    "result": {
        "sub_task_stats": [
            "SUCCESS",
            "STARTED"
        ]
    }
}

// Completed
{
<strong>    "statusCode": 200,
</strong>    "message": "Get pipeline status successfully.",
    "result": {
        "status": "synchronized" // synchronized
    }
}
</code></pre>

### Delete Knowledge Base

**Request:**

```sh
curl -X DELETE https://etl.epsilla.com/api/v1/datasources/<project_id>/pipeline/<datasource_id> \
     -H "X-API-Key: <Project-API-Key>" 
```

**Response:**

```json
{
    "statusCode": 200,
    "message": "Delete data source successfully."
}
```
