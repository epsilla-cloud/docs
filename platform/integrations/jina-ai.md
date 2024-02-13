# Jina AI

Epsilla integrates with Jina AI with the **jinaai/jina-embeddings-v2-base-en, jinaai/jina-embeddings-v2-base-zh**, and **jinaai/jina-embeddings-v2-small-en** embedding model.

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../../vector-database/embeddings.md#jina-ai-embedding).

On Epsilla Cloud, you can enable Jina AI integration by providing your Jina AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2023-12-29 at 11.41.15 PM.png" alt=""><figcaption></figcaption></figure>

Then you can start using the jinaai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-10 at 10.52.40 AM.png" alt=""><figcaption></figcaption></figure>
