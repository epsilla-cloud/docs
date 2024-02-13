# Nomic AI

Epsilla integrates with Nomic AI with the following embedding models.

| Name                            | Dimensions |
| ------------------------------- | ---------- |
| **nomicai/nomic-embed-text-v1** | 768        |

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../../vector-database/embeddings.md#nomic-ai-embedding).

On Epsilla Cloud, you can enable Nomic AI integration by providing your Nomic AI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.21.53 AM.png" alt=""><figcaption></figcaption></figure>

Then you can start using the nomicai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-13 at 11.23.30 AM.png" alt=""><figcaption></figcaption></figure>
