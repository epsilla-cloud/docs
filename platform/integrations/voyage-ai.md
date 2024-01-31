# Voyage AI

Epsilla integrates with Voyage AI with the **voyageai/voyage-2** and **voyageai/voyage-code-2,** and **voyageai/voyage-lite-02-instruct** embedding model.

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../../vector-database/embeddings.md#voyage-ai-embedding).

On Epsilla Cloud, you can enable Jina AI integration by providing your Voyage AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-10 at 10.54.00 AM.png" alt=""><figcaption></figcaption></figure>

Then you can start using the voyageai-02 embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-31 at 12.10.07 PM.png" alt=""><figcaption></figcaption></figure>
