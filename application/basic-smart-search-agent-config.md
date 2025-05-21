# Basic Smart Search Agent Config

Following the previous steps, once the smart search agent is created, its basic settings are prefilled based on the initial configuration.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.07.10 PM.png" alt="" width="563"><figcaption></figcaption></figure>

This guide provides a step-by-step overview of how to configure and fine-tune the smart search agent's behavior and capabilities by adjusting all the configurations. When the configuration is changed, you can immediately see the result from the Preview tab on the right.

### Smart Search Agent Name

This is the name of the smart search agent. It will be displayed as the agent’s identity when interacting with users.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.08.59 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Smart Search Agent Description

This field defines the purpose of the smart search agent. Provide a brief explanation of what the agent is designed to do, so users know its capabilities.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.09.32 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Choosing the LLM for Generating Answer

This field allows you to select which large language model the smart search agent will use to answer the user question.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.12.18 PM.png" alt="" width="340"><figcaption></figcaption></figure>

When your chatbot uses epsilla/gpt-4o  models, every message or request sent to the LLM is tracked and counts towards your monthly usage limit, which is based on [how many messages your plan allows](../billing-management.md#tracking-current-plan-usage).

If you want to use a different model, you can bring your own API keys for other LLMs, such as those from OpenAI or Anthropic. In this case, the cost of using those external models (measured by the number of tokens processed) will be covered by you, directly through the API provider. This means that when using your own keys, the usage does not affect your Epsilla monthly message quota.

### Configuring Knowledge for the Smart Search Agent

This section allows you to connect one or more knowledge bases to the smart search agent, enabling it to reference specific information when answering user queries.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.56.41 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Adding a Knowledge Base**

1. Click on the dropdown under "Add Knowledge Base" to see the list of available knowledge bases that have already been created.
2. Select the desired knowledge base from the list.
3. You can add multiple knowledge bases by repeating the above steps.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.56.58 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Removing a Knowledge Base**

1. If you wish to remove a knowledge base, click on the trash icon next to the selected knowledge base.
2. This will detach the selected knowledge base, preventing the chatbot from using that source for future queries.

**Configuring Advanced Knowledge Retrieval**

The knowledge retriever is responsible for fetching relevant information from the connected knowledge bases during the smart search agent's interaction. For use cases that need a high knowledge retrieval quality, the advanced section allows you to configure how the system searches and retrieves information to ensure the chatbot provides the most relevant responses.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.57.58 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **HyDE (Hypothetical Document Embeddings):** HyDE is a feature that can be enabled to refine retrieval by generating a hypothetical document based on the query. The generated document is then used to search the knowledge base, improving the accuracy of retrieval. You can toggle this option depending on whether you need this functionality for deeper search optimization. You can even customize the prompt for HyDE, and choose which LLM to power the generation.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.00.08 AM.png" alt="" width="563"><figcaption></figcaption></figure>

For each knowledge base you add, a corresponding retriever is automatically added. These retrievers are numbered sequentially (e.g., Retriever 1, Retriever 2) based on the order of the added knowledge bases. Each retriever fetches information from its assigned knowledge base and can be individually configured to optimize how data is retrieved:

* **Source Knowledge Base:** This is the knowledge base from which the retriever should pull information.
* **Similarity Search Function:** This option determines how the retriever identifies relevant records from the knowledge base. You can select between different methods:
  * **Semantic Similarity (Dense Vector Embeddings):** The system will use vector embeddings to measure how semantically similar the input query is to the records in the knowledge base. This is ideal for understanding the meaning of the query in context.
  * (Coming soon) Other options include keyword search functions, but dense vector embeddings offer a deeper level of understanding.
* **Number of Candidates:** This field controls how many records the retriever should pull from the knowledge base based on best match of chosen similarity search function. You can increase or decrease this number based on how many records you want the model to consider. The default value is 10.
* **Retriever Type:** How to retrieve the records from the knowledge base.
  * **Basic Retriever:** The system retrieves the records as-is, without any further processing.
  * (Coming soon) Other options: You may have more advanced retriever types depending on your specific use case, such as sentence-window retriever and auto-merging retriever.
* **Filter (Optional):** If you want to apply semantic distance filters and meta data filters to refine the retrieved results, you can use this field.
  * **Example:** You can add a filter like `@distance < 0.7` to ensure that only records with a certain level of similarity (based on the distance between vectors) are returned. You can add a meta data filter like `Conference LIKE '%NeurIPS%'` to constrain the results to only those documents that are published on the NeurIPS conference.
  * You can also provide filters dynamically through an API payload when integrating external systems with the smart search agent. This allows the smart search agent’s behavior to adapt in real-time, making its responses more flexible and tailored to specific contexts or user queries.

A reranker reorganizes the results retrieved by the smart search agent, prioritizing them based on their relevance to the user’s query. By applying different reranking methods, the reranker ensures that the most relevant and useful information is surfaced first, improving the overall quality of the smart search agent's responses. When you have only one retriever, using a reranker is optional. However, if your smart search agent is connected to multiple knowledge bases (resulting in multiple retrievers), enabling a reranker becomes essential to effectively combine and rank the results from each retriever.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.04 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Semantic Distance:** This method ranks the results based on their semantic closeness to the query. It uses vector embeddings to determine how conceptually similar each document is to the query.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.12 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Reciprocal Rank Fusion (RRF):** RRF aggregates the rankings from multiple retrievers. It favors documents that appear high in multiple retriever lists. The rerank constant can be adjusted to control how much emphasis is placed on the ranking order from each retriever. This option allows you to assign different weights to the results from each retriever, helping you prioritize the retrievers that should have a stronger influence on the final ranking.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.25 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Relative Score Fusion (RSF):** RSF calculates the relative scores of documents across retrievers and reranks them based on the weighted score, ensuring the most relevant documents surface higher in the results.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.32 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Jina AI Reranker:** This reranker leverages a pre-trained Jina AI reranker model, such as `jinaai/jina-reranker-v1-base-en`, to reorder documents with a learned ranking model. It applies more sophisticated machine learning techniques for reranking based on training data.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.43 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Configuring Smart Search Agent Appearance

The appearance configuration allows you to customize the look and feel of the smart search agent interface, ensuring that it aligns with your brand and provides an engaging user experience.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.23.14 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Add Smart Search Icon:** This option allows you to upload a custom icon for the smart search agent, which will be displayed in the search window. This icon helps personalize the smart search agent and make it easily recognizable for users.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.23.23 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Primary Color:** The primary color defines the dominant color theme for the smart search agent's interface. It influences various elements such as reference cards and related questions.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.25.01 PM (1).png" alt="" width="563"><figcaption></figcaption></figure>

### Customizing the Search Experience

Epsilla provides multiple options to fine-tune the search experience, allowing you to personalize how the smart search agent interacts with users and adjust key interface elements. Below are the key settings you can configure to create a seamless and engaging search interface:

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.27.42 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Chatbot Introduction Message:** This is the initial message the chatbot sends when a user opens the chat window. It acts as a welcome message, giving the user an idea of what the chatbot can help with.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.03.19 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Searchbox Placeholder:** This is the placeholder text that appears in the search input box before a user starts typing. It gives users a hint about what they can ask.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.29.03 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Sample Questions:** This feature allows you to predefine a set of sample questions that appear as clickable suggestions below the searchbox. These suggestions help guide users who might not know what to ask or who need a starting point.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.30.00 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Generate Answer** controls how the smart search agent responds to user queries. When enabled (by default), the agent uses retrieved search results to construct responses, ensuring answers are grounded in the provided information. It uses placeholders like `<SEARCH_RESULT>` and`<USER_QUESTION>` to integrate the retrieved data and user question into the prompt. If the feature is disabled, the agent will respond by directly providing the search results without generating an answer.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.32.50 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Generate Follow-Up Questions:** This setting enables the smart search app to automatically generate follow-up questions based on the user’s question and the agent's answer. The questions are intended to keep the conversation flowing and prompt deeper engagement. You can even customize the prompt, and choose which LLM to power the generation.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.40.20 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Hide Epsilla Logo:** Toggling this option allows you to hide the Epsilla branding from the search interface, making the experience more custom to your brand. This is only available for Professional tier and Enterprise tier customers.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.07.30 AM.png" alt="" width="551"><figcaption></figcaption></figure>

* **Collect User Feedback:** When this option is enabled (by default), users can provide feedback on the smart search agent's responses. Feedback buttons (e.g., thumbs up, thumbs down) appear below each message, helping you assess the smart search agent’s performance.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.41.54 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Advanced Settings Documentation

The Advanced Settings section allows fine-tuning of your smart search agent's behavior for specific use cases. These advanced settings offer enhanced control over smart search agent behavior, ensuring a customized experience aligned with specific needs and optimizing the flow of information between the user and the smart search agent.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.43.03 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Rewrite User Question:** When enabled, the chatbot can **rewrite the user's question**. This setting is particularly useful for improving the smart search agent’s understanding of the user questions. You can even customize the prompt, and choose which LLM to power the query rewriting.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.44.48 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Execution Timeout (Seconds):** This setting allows you to define how long the smart search agent should wait for a response to process before timing out. This can help prevent system overloads or endless waits for responses from external systems. Default timeout is set to 180 seconds, but this can be adjusted depending on the complexity of the queries and your system's performance.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.19.02 AM.png" alt="" width="563"><figcaption></figcaption></figure>
