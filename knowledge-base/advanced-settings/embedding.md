# Embedding

**Embedding** setting allows users to select specific embedding models for efficient text representation, improving search quality.

### Choose Embedding Model

Choose an embedding model from the dropdown to use for embedding data chunks:

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-30 at 1.45.29 AM.png" alt="" width="563"><figcaption></figcaption></figure>

The default **epsilla/text-embedding-3-small** and **epsilla/text-embedding-3-large** models leverage Epsilla's built-in OpenAI integration and do not require any additional config from user side. However, if you choose other embedding models, you must first add an integration for the respective vendors:

<figure><img src="../../.gitbook/assets/Screenshot 2024-09-30 at 1.51.28 AM.png" alt="" width="375"><figcaption></figcaption></figure>

Read more about [embedding](../../epsilla-vector-database/advanced-topics/embeddings.md).

### Which Embedding Model Fits My Needs Best

When selecting an embedding model for your specific use case, it's important to recognize that there is no one-size-fits-all model. The ideal model depends on factors such as the nature of your use case, cost considerations, and performance requirements. OpenAI offers large and small embedding models: the large embedding model excels in general-purpose scenarios where higher quality is crucial, while the smaller model is a more cost-efficient option for use cases with tighter budget constraints. JinaAI provides embedding models well-suited for multilingual applications, making them an excellent choice for use cases involving diverse languages. For more specialized needs, VoyageAI models are optimized for vertical domains, such as financial or legal contexts, offering domain-specific insights and improved accuracy in these areas.

For an overview of different models' performance across various benchmarks, you can refer to the [MTEB leaderboard](https://huggingface.co/spaces/mteb/leaderboard). However, it's important not to blindly rely on these results, as the datasets used in MTEB might not fully represent your specific use case and could be biased. Always consider evaluating models in the context of your own data and requirements.

