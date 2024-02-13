# OpenAI

On Epsilla Cloud, you can enable OpenAI integration by providing your OpenAI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2023-12-29 at 11.36.48 PM.png" alt=""><figcaption></figcaption></figure>

## Embeddings

Epsilla integrates with OpenAI with the following embedding models:

| Name                              | Dimensions |
| --------------------------------- | ---------- |
| **openai/text-embedding-3-large** | 3072       |
| **openai/text-embedding-3-small** | 1536       |
| **openai/text-embedding-ada-002** | 1536       |

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../../vector-database/embeddings.md#openai-embedding).

Then you can start using the openai embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-31 at 12.10.57 PM.png" alt=""><figcaption></figcaption></figure>
