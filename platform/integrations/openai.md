# OpenAI

Epsilla integrates with OpenAI with the **text-embedding-3-large**, **text-embedding-3-small**, and **text-embedding-ada-002** embedding model.

For Epsilla open source vector db, you just need to add a header in the data ingestion and semantic search queries [like this](../../vector-database/embeddings.md#openai-embedding).

On Epsilla Cloud, you can enable OpenAI integration by providing your OpenAI API key (we securely manage your keys using AWS KMS):

<figure><img src="../../.gitbook/assets/Screenshot 2023-12-29 at 11.36.48 PM.png" alt=""><figcaption></figcaption></figure>

Then you can start using the text-embedding-ada-002 embedding model during vector table schema creation:

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-31 at 12.10.57 PM.png" alt=""><figcaption></figcaption></figure>
