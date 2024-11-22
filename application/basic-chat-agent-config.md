# Basic Chat Agent Config

Following the previous steps, once the chat agent is created, its basic settings are prefilled based on the initial configuration.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.38.36 AM.png" alt="" width="563"><figcaption></figcaption></figure>

This guide provides a step-by-step overview of how to configure and fine-tune the chat agent’s behavior and capabilities by adjusting all the configurations. When the configuration is changed, you can immediately see the result from the Preview tab on the right.

### Chatbot Name

This is the name of the chat agent. It will be displayed as the agent’s identity when interacting with users.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.38.52 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Chatbot Description

This field defines the purpose of the chat agent. Provide a brief explanation of what the chat agent is designed to do, so users know its capabilities.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.38.57 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Assigning a Role to the Chatbot

This is a critical configuration that allows you to set the chat agent's role. The role is used to instruct the LLM on how to respond to user queries, giving context to the chat agent's behavior. This description acts as a "persona" for the chat agent.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.39.04 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Choosing the Brain (LLM) for the Chatbot

This field allows you to select which large language model the chat agent will use to answer the user question.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.40.03 AM.png" alt="" width="437"><figcaption></figcaption></figure>

When your chat agent uses epsilla/gpt-4o  models, every message or request sent to the LLM is tracked and counts towards your monthly usage limit, which is based on [how many messages your plan allows](../billing-management.md#tracking-current-plan-usage).

If you want to use a different model, you can bring your own API keys for other LLMs, such as those from OpenAI or Anthropic. In this case, the cost of using those external models (measured by the number of tokens processed) will be covered by you, directly through the API provider. This means that when using your own keys, the usage does not affect your Epsilla monthly message quota.

### Configuring Knowledge for the Chatbot

This section allows you to connect one or more knowledge bases to the chat agent, enabling it to reference specific information when answering user queries.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.56.41 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Adding a Knowledge Base**

1. Click on the dropdown under "Add Knowledge Base" to see the list of available knowledge bases that have already been created.
2. Select the desired knowledge base from the list.
3. You can add multiple knowledge bases by repeating the above steps.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.56.58 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Removing a Knowledge Base**

1. If you wish to remove a knowledge base, click on the trash icon next to the selected knowledge base.
2. This will detach the selected knowledge base, preventing the chat agent from using that source for future queries.

**Configuring Advanced Knowledge Retrieval**

The knowledge retriever is responsible for fetching relevant information from the connected knowledge bases during the chat agent's interaction. For use cases that need a high knowledge retrieval quality, the advanced section allows you to configure how the system searches and retrieves information to ensure the chat agent provides the most relevant responses.

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
  * **Hypothetical Question Retriever:** The system retrieves the [generated hypothetical questions](../knowledge-base/advanced-settings/hypothetical-questions.md)  via semantic search first, then traces back to the original documents.
  * (Coming soon) Other options: You may have more advanced retriever types depending on your specific use case, such as sentence-window retriever and auto-merging retriever.
* **Filter (Optional):** If you want to apply semantic distance filters and meta data filters to refine the retrieved results, you can use this field.
  * **Example:** You can add a filter like `@distance < 0.7` to ensure that only records with a certain level of similarity (based on the distance between vectors) are returned. You can add a meta data filter like `Filename LIKE '%Instruction 1040%'` to constrain the results to only those documents related to IRS Instruction 1040, ensuring the chat agent retrieves information from highly relevant documents.
  * You can also provide filters dynamically through an API payload when integrating external systems with the chat agent. This allows the chat agent’s behavior to adapt in real-time, making its responses more flexible and tailored to specific contexts or user queries.

A reranker reorganizes the results retrieved by the chat agent, prioritizing them based on their relevance to the user’s query. By applying different reranking methods, the reranker ensures that the most relevant and useful information is surfaced first, improving the overall quality of the chat agent's responses. When you have only one retriever, using a reranker is optional. However, if your chat agent is connected to multiple knowledge bases (resulting in multiple retrievers), enabling a reranker becomes essential to effectively combine and rank the results from each retriever.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.04 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Semantic Distance:** This method ranks the results based on their semantic closeness to the query. It uses vector embeddings to determine how conceptually similar each document is to the query.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.12 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Reciprocal Rank Fusion (RRF):** RRF aggregates the rankings from multiple retrievers. It favors documents that appear high in multiple retriever lists. The rerank constant can be adjusted to control how much emphasis is placed on the ranking order from each retriever. This option allows you to assign different weights to the results from each retriever, helping you prioritize the retrievers that should have a stronger influence on the final ranking.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.25 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Relative Score Fusion (RSF):** RSF calculates the relative scores of documents across retrievers and reranks them based on the weighted score, ensuring the most relevant documents surface higher in the results.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.32 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Jina AI Reranker:** This reranker leverages a pre-trained Jina AI reranker model, such as `jinaai/jina-reranker-v1-base-en`, to reorder documents with a learned ranking model. It applies more sophisticated machine learning techniques for reranking based on training data.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 12.59.43 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Tools

The **Tools** section allows you to enhance the AI agent's capabilities by integrating additional skills. These tools enable the chat agent to perform specialized tasks, such as retrieving real-time information from the internet or accessing external systems, ensuring more dynamic and contextually relevant interactions.

<figure><img src="../.gitbook/assets/Screenshot 2024-11-22 at 12.52.44 AM.png" alt="" width="563"><figcaption></figcaption></figure>

#### **Search the Internet**

<figure><img src="../.gitbook/assets/Screenshot 2024-11-22 at 12.53.58 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* The **Search the Internet** tool enables your chat agent to retrieve relevant information from the web. This feature can be customized to focus on specific domains or perform general searches. Below are the configurable settings:
  * **Enable/Disable Search**: Toggle the tool on or off to activate or deactivate internet search capabilities for the chat agent.
  * **Max Number of Results**: Define the maximum number of results the search should return. For example, you can set it to 5 to limit the number of results retrieved.
  * **Advanced Search**: Enable or disable advanced search options for more refined queries.
  * **Focus Search**: Narrow down search results by specifying one or more focus domains. For instance, you can add a domain such as `https://stackoverflow.com` to constrain retrieving results from that specific site. If leaving empty, the search will be from the whole internet.

### Configuring Chatbot Appearance

The appearance configuration allows you to customize the look and feel of the chat agent interface, ensuring that it aligns with your brand and provides an engaging user experience.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.33.19 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Add Chatbot Icon:** This option allows you to upload a custom icon for the chat agent, which will be displayed in the chat window. This icon helps personalize the chat agent and make it easily recognizable for users.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.33.29 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Primary Color:** The primary color defines the dominant color theme for the chat agent's interface. It influences various elements such as message buttons or key highlights.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.34.16 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Background Color:** This option allows you to set the background color for the chat window. You can select a color that matches your website's or brand’s theme for a consistent user experience.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.34.43 AM.png" alt="" width="563"><figcaption></figcaption></figure>

*   **User Message Style:** You can customize the appearance of user messages by selecting a background color, adjusting the border radius, or show/hide user avatar.

    * **Background Color:** Choose the color of the message bubbles for user inputs.

    <figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.36.18 AM.png" alt="" width="563"><figcaption></figcaption></figure>

    * **Border Radius:** Control the roundness of the message bubbles. Higher values result in more rounded edges.

    <figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.36.58 AM.png" alt="" width="563"><figcaption></figcaption></figure>

    * **Hide User Avatar:** Don't show user avatar for user messages

    <figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.37.25 AM.png" alt="" width="563"><figcaption></figcaption></figure>
*   **Bot Message Style:** Customize how the chat agent's responses appear in the chat. You can hide the message box background or use the default color for bot buttons.

    * **Hide Message Box Background:** You can toggle this setting to remove the background from bot messages, making them appear directly on the chat background.

    <figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.38.55 AM.png" alt="" width="563"><figcaption></figcaption></figure>

    * **Use Default Color for Bot Buttons:** Enabling this option will apply the default button colors to the action buttons below the chat agent's response messages.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 1.38.30 AM (1).png" alt="" width="563"><figcaption></figcaption></figure>

### Customizing the Chat Experience

Epsilla provides multiple options to fine-tune the chat experience, allowing you to personalize how the chat agent interacts with users and adjust key interface elements. Below are the key settings you can configure to create a seamless and engaging chat interface:

<figure><img src="../.gitbook/assets/Screenshot 2024-11-03 at 4.09.49 PM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Chatbot Introduction Message:** This is the initial message the chat agent sends when a user opens the chat window. It acts as a welcome message, giving the user an idea of what the chat agent can help with.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.03.19 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Chatbox Placeholder:** This is the placeholder text that appears in the chat input box before a user starts typing. It gives users a hint about what they can ask.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.03.40 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Sample Questions:** This feature allows you to predefine a set of sample questions that appear as clickable suggestions below the chatbox. These suggestions help guide users who might not know what to ask or who need a starting point.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.04.12 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Citations:** Users can configure how citations appear and interact within chat responses. These settings offer flexibility to tailor the presentation of sources and references.

In the **How to show citations** option, users can select between two main display styles: a simple **Quotation Mark** style or a more detailed **Card** style. Quotation Mark is the default choice.

<figure><img src="../.gitbook/assets/Screenshot 2024-11-03 at 4.18.10 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The **Card** style includes a brief title and description of the knowledge record, limited to three lines for readability. Additionally, users can choose to display a **Thumbnail** image along with the title, enhancing the visual context of the citation.

<figure><img src="../.gitbook/assets/Screenshot 2024-11-03 at 4.19.24 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The **Behavior when clicking on a citation** setting controls when user click a citation in the message, how to show citation details in the drawer. By default, Epsilla will decide automatically. It will highlight PDF, or show the knowledge record content directly for non-PDF files.

<figure><img src="../.gitbook/assets/Screenshot 2024-11-03 at 4.20.32 PM.png" alt="" width="563"><figcaption></figcaption></figure>

When choosing **Webpage of the Provided URL**, Epsilla will fetch the linked webpage from the configured **URL field**  in the knowledge record and render the webpage.

<figure><img src="../.gitbook/assets/Screenshot 2024-11-03 at 4.21.17 PM (1).png" alt="" width="563"><figcaption></figcaption></figure>

* **Generate Follow-Up Questions:** This setting enables the chat agent to automatically generate follow-up questions based on the user’s previous queries. The questions are intended to keep the conversation flowing and prompt deeper engagement. You can even customize the prompt, and choose which LLM to power the generation.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.05.14 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **How to Label a Chat:** This option allows you to set a rule for how chats should be labeled in the chat history. Labels can be automatically generated based on the conversation's content or time.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.06.18 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Hide Epsilla Logo:** Toggling this option allows you to hide the Epsilla branding from the chat interface, making the experience more custom to your brand. This is only available for Professional tier and Enterprise tier customers.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.07.30 AM.png" alt="" width="551"><figcaption></figcaption></figure>

* **Collect User Feedback:** When this option is enabled (by default), users can provide feedback on the chat agent's responses. Feedback buttons (e.g., thumbs up, thumbs down) appear below each message, helping you assess the chat agent's performance.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.06.57 AM (1).png" alt="" width="563"><figcaption></figcaption></figure>

* **Allow Message Sharing:** This option enables users to share chat agent messages with others, either through social media or other platforms. It adds share icons to the chat agent interface, increasing the reach of helpful information.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.07.11 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Advanced Settings Documentation

The Advanced Settings section allows fine-tuning of your chat agent's behavior for specific use cases. These advanced settings offer enhanced control over chat agent behavior, ensuring a customized experience aligned with specific needs and optimizing the flow of information between the user and the chat agent.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.18.19 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Prompt Template** controls how the chat agent responds to user queries. The template is designed to provide context based on both the **chat history** and **related knowledge** retrieved by the chat agent. The format includes placeholders like `<CHAT_HISTORY>`, `<RELATED_KNOWLEDGE>`, and `<USER_QUESTION>` to ensure the chat agent provides grounded responses based on the user's context.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.18.32 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Chat History** setting allows the chat agent to remember a portion of the conversation, helping it maintain context.
  * **Most Recent Rounds**: Choose how many previous messages are remembered in the chat. Default to 5 rounds.
  * (Coming soon) Other options include getting the most semantically relevant rounds of messages, or do a summarization of the conversation.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.18.45 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Rewrite User Question:** When enabled, the chat agent can **rewrite the user's question**. This setting is particularly useful for improving the chat agent's understanding of the user questions. You can even customize the prompt, and choose which LLM to power the query rewriting.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.18.55 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Execution Timeout (Seconds):** This setting allows you to define how long the chat agent should wait for a response to process before timing out. This can help prevent system overloads or endless waits for responses from external systems. Default timeout is set to 180 seconds, but this can be adjusted depending on the complexity of the queries and your system's performance.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-17 at 2.19.02 AM.png" alt="" width="563"><figcaption></figcaption></figure>
