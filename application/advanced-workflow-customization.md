# Advanced Workflow Customization

The **Advanced Workflow Customization** feature in Epsilla is designed for users who require advanced customization of their AI agents. This mode allows you to go beyond the default settings, giving you control over the flow of data, responses, and actions your AI agent takes. Users can create sophisticated interactions, optimize the logic of queries, and fine-tune the behavior of their AI agent.

### **Who Should Use This?**

This feature is ideal for:

* **Savvy GenAI Builders**: Users who have experience building generative AI agents and need more control over the workflow for fine-tuning responses.
* **AI Experts**: Professionals seeking to optimize data retrieval, integrate complex decision-making paths, or enhance the overall user interaction experience with their AI agents.

### **Enable Edit Workflow**:

* Locate the "Edit Workflow" toggle at the bottom of the settings panel.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 12.41.49 AM (1).png" alt=""><figcaption></figcaption></figure>

* Switch the toggle from "Off" to "On" to activate the workflow editor.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 12.48.31 AM.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
The workflow view offers a higher degree of flexibility for customizing your AI agent. However, once you enter the workflow view, you cannot revert to the normal view without losing all customizations made in the workflow view. This is because workflow customizations involve advanced settings that the normal view cannot support.
{% endhint %}

### Track Data Flow in Workflow

When you run the agent by sending a query in the Preview on the right, you can visualize the entire journey of data as it moves from user input through each node of the workflow graph, all the way to the final agent output. This powerful tool provides real-time insights into the intermediate results at each stage, enabling users to understand how data is processed, transformed, and used within the workflow. By observing the outputs at each node, you can fine-tune your workflow, optimize logic, and ensure the AI agent behaves as expected, enhancing overall performance and accuracy.

{% embed url="https://youtu.be/73Y8IsHYyMM" %}

### Modify Workflow

To edit a workflow in Epsilla, follow these steps for adding, editing, and deleting nodes:

**Adding Components**:

* Click on the "Add Components" button in the workflow view.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 2.10.22 AM.png" alt="" width="360"><figcaption></figcaption></figure>

* Select a category from the options (e.g., Data, Retrieval, LLM, Logic).

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 2.11.12 AM.png" alt="" width="195"><figcaption></figcaption></figure>

* Drag the desired component, such as a "Knowledge Base" or "Basic Retriever," into the workflow area to incorporate new functionality.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 2.11.57 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Connecting Two Components**

* Drag from the output of one component to the input of another component to connect the output and the input. Please make sure the data types are compatible.

**Editing Components**

* Click on a node within the workflow to adjust inputs, outputs, and other parameters directly in this panel to customize the node’s behavior according to your needs.

**Deleting or Duplicating Nodes**

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 2.13.34 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* Right-click on a node to access additional options.
* Select "Delete" to remove the node from the workflow, or choose "Duplicate" to create a copy of the node with the same configuration.

**Disconnect Two Components**

* Click the "cross" button on the edge to disconnect two components.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 2.19.07 AM.png" alt="" width="477"><figcaption></figcaption></figure>

### Deep Dive into the Default Chat Agent Workflow&#x20;

#### 1. **Workflow Input**

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.06.47 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Functionality**: This component represents the starting point of the workflow. It captures the input message from the user, which initiates the workflow process.
* `user_message`—this variable holds the content of the user's input message. `user_message` is passed through the workflow to be processed in subsequent nodes.

#### 2. **Knowledge Base, Basic Retriever, and Document String Reducer**

This section is responsible for empower the chat agent with data and knowledge.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.07.49 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Knowledge Base**:
  * **Functionality**: This stores the data and knowledge the AI agent uses to find relevant information. You can choose from the dropdown list that is created in [Knowledge Base](../knowledge-base/) section.
  * `Semantic Search Index`—a representation of indexed data for semantic retrieval.
* **Basic Retriever**:
  * **Functionality**: The Basic Retriever searches the Knowledge Base for relevant documents based on the user query. It extracts the most relevant information to answer the user's question.
  * **Inputs**:
    * `Query`—typically derived from the user message.
    * `Search Index`—connects to the `Semantic Search Index` from the Knowledge Base.
    * `Limit`—the number of top results to retrieve.
    * `Filter`—any meta data filtering conditions to refine the search.
  * **Outputs**: `Search Result`—a set of the most relevant documents that match the query.
* **Document String Reducer**
  * **Functionality**: This node converts the retrieved documents (chunks) into a string format, making them ready for further processing. It allows formatting of document content to be used by the AI agent. It features a template string to specify how each chunk should be converted to a string. Then the list of chunks will be concat into a single string.
  * **Inputs**: `Documents`—a list of documents (chunks) retrieved by the Basic Retriever.
  * **Outputs**: `Reduced String`—a formatted string converted from the documents.

#### 3. **Window Buffer Chat History and Message String Reducer**

This section is responsible for maintaining the conversation memory of the chat agent.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.07.59 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Window Buffer Chat History**
  * **Functionality**: This component keeps track of recent messages in the conversation, maintaining a context of prior interactions between the user and the AI agent.
  * **Inputs**:
    * `User Message`—the latest message from the user (to be stored for future conversation).
    * `AI Response Message`—the response from the AI **after** this round conversation finishes (notice it is connected back from the Workflow output).
    * `Buffer Size`—defines how many past messages to retain for context.
  * **Outputs**: `Chat History`—a sequence of recent conversation exchanges that helps maintain context during ongoing interactions.
* **Message String Reducer**
  * **Functionality**: Converts a list of chat messages into a single string, allowing the AI to process previous interactions as a consolidated context. It features a template string to specify how each message should be converted to a string. Then the list of chunks will be concat into a single string.
  * **Inputs**: `Messages`—the set of messages from the chat history.
  * **Outputs**: `Reduced String`—a single, formatted string representing the recent conversation context.

#### 4. **String Template and LLM Completion**

This section is responsible for generating the answer.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.08.29 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* #### **String Template**
  * **Functionality**: Generates a string by combining various pieces of data like chat history, retrieved knowledge, and the user’s question. This string serves as the **prompt** for the LLM, ensuring that the generated response is grounded in context.
  * **Inputs**:
    * `chat_history`—from the `Message String Reducer`.
    * `retrieved_knowledge`—from the `Document String Reducer`.
    * `the_question`—the original user question.
  * **Outputs**: `Rendered String`—a prompt ready for the LLM, incorporating the context, relevant knowledge, and the user's question.
* #### **LLM Completion**
  * **Functionality**: This is where the large language model (LLM) processes the structured prompt and generates a response. The LLM uses the input data to produce a coherent answer based on the user's query and the provided knowledge.
  * **Inputs**:
    * `System Message`—guidance for the AI's role and behavior.
    * `User Message`—the prompt from the `String Template`.
    * `LLM`—the model used (e.g., `openai/gpt-4o`).
    * `Temperature`—controls the randomness of the response.
    * `Max Token`—the maximum length of the generated response.
  * **Outputs**: `Generated Result`—the LLM's response based on the inputs.

#### 8. **Workflow Output**

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.08.36 AM.png" alt="" width="384"><figcaption></figcaption></figure>

* **Functionality**: This node collects the final processed output from the workflow, preparing it to be sent back to the user. It serves as the endpoint where the workflow concludes.
* **Collected Values**:
  * `final_output`—the response generated by the LLM.
  * `knowledge`—stores the data and knowledge retrieved from knowledge base. It is used for showing the references and future inspection in evaluation.
* **Workflow Execution Results**: `final_output` and `knowledge`—these are presented to the user as the final answer.

### Deep Dive into the Default Smart Search Agent Workflow&#x20;

**1. Workflow Input**

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.34.09 AM.png" alt="" width="314"><figcaption></figcaption></figure>

* **Functionality**: This component captures the user's input message, initiating the workflow. In this case, it starts with the `question` variable.
* **Input Variables**: `question`—this holds the content of the user's query. `question` is passed through the workflow for further processing.

**2. Knowledge Base, Basic Retriever, and Document String Reducer**

These elements empower the Smart Search Agent with data and knowledge.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.34.17 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Knowledge Base**:
  * **Functionality**: This stores the data and knowledge the AI agent uses to find relevant information. You can choose from the dropdown list that is created in [Knowledge Base](../knowledge-base/) section.
  * `Semantic Search Index`—a representation of indexed data for efficient semantic retrieval.
* **Basic Retriever**:
  * **Functionality**: Searches the Knowledge Base for documents that match the user's query. It extracts the most relevant information to answer the user's question.
  * **Inputs**:
    * `Query`—typically the user question.
    * `Search Index`—connected to the `Semantic Search Index`.
    * `Limit`—number of top results to retrieve.
    * `Filter`—meta data filtering conditions to refine the search.
  * **Outputs**: `Search Result`—a set of documents that match the query.
* **Document String Reducer**:
  * **Functionality**: This node converts the retrieved documents (chunks) into a string format, making them ready for further processing. It allows formatting of document content to be used by the AI agent. It features a template string to specify how each chunk should be converted to a string. Then the list of chunks will be concat into a single string.
  * **Inputs**: `Documents`—a list retrieved by the Basic Retriever.
  * **Outputs**: `Reduced String`—a formatted string containing the consolidated content.

**3. String Template and LLM Completion**

This section generates the response using the information retrieved from the knowledge base.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.34.25 AM.png" alt="" width="520"><figcaption></figcaption></figure>

* **String Template**:
  * **Functionality**: Combines retrieved knowledge and the user’s question into a structured prompt, ensuring that the AI's answer is contextually grounded.
  * **Inputs**:
    * `retrieved_knowledge`—from the Document String Reducer.
    * `the_question`—the user’s original question.
  * **Outputs**: `Rendered String`—the generated prompt for the LLM.
* **LLM Completion**:
  * **Functionality**: Processes the prompt using the LLM (e.g., `openai/gpt-4o`) to generate a coherent response.
  * **Inputs**:
    * `User Message`—the structured prompt from the String Template.
    * `LLM`—the selected model.
    * `Temperature`—adjusts the randomness of responses.
    * `Max Token`—sets the response length.
  * **Outputs**: `Generated Result`—the AI's answer based on the prompt.

**4. Additional String Template, LLM Completion, and String Splitter**

This sequence helps generate follow-up questions and structure them for display.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.34.37 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **String Template for Follow-up**:
  * **Functionality**: Prepares a prompt to generate additional questions that guide the user through related or deeper topics.
  * **Inputs**: `the_question`, `the_answer`, `retrieved_knowledge`.
  * **Outputs**: `Rendered String`—the structured prompt for the LLM.
* **LLM Completion for Follow-up**:
  * **Functionality**: Generates possible follow-up questions using a smaller model (e.g., `openai/gpt-4o-mini`) to keep responses brief and to the point.
  * **Inputs**:
    * `User Message`—the prompt from the follow-up String Template.
    * `Temperature`—for varied suggestions.
    * `Max Token`—limited to ensure concise outputs.
  * **Outputs**: `Generated Result`—suggested follow-up questions.
* **String Splitter**:
  * **Functionality**: Splits the generated list of follow-up questions into individual entries for easier presentation.
  * **Inputs**:
    * `Input String`—the list of questions.
    * `Separator`—defines how to split the string.
    * `Limit`—controls the number of items.
  * **Outputs**: `Splitted List`—individual questions formatted for display.

{% hint style="info" %}
When generate follow-up questions is enabled for chat agent, the chat agent workflow will also contain this part.
{% endhint %}

**5. Workflow Output and Search Result Store**

Finalizes the output, stores results for reference, and displays the answer and follow-up questions to the user.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.34.44 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* **Workflow Output**:
  * **Functionality**: Prepares the final results, including the AI's generated answer and any follow-up questions.
  * **Collected Values**:
    * `Search Result`—documents retrieved during the search.
    * `Generated Answer`—the main response from the LLM.
    * `Follow-up Questions`—suggestions for further inquiries.
  * **Outputs**: `final_output` for user display, and `knowledge` for reference and evaluation.
* **Search Result Store**:
  * **Functionality**: Keeps a record of the user's query, the AI's answer, and the relevant references and follow-up questions. This allows for easy retrieval and analysis of past interactions.
  * **Inputs**:
    * `Question`—the user’s original query.
    * `Answer`—the LLM's response.
    * `References`—links to the relevant knowledge used.
    * `FollowUpQuestions`—additional questions for the user.
  * **Outputs**: Stores all data for future reference and analysis.

### Adapting Workflow for Configuration Changes

If specific configurations are enabled in the normal view, corresponding sections will appear when you switch to the workflow view.

**Example 1: Enabling User Query Rewrite**

When [**Rewrite User Question**](basic-chat-agent-config.md#advanced-settings-documentation) is activated, the workflow adds steps to refine user input. A **String Template** and **LLM Completion** are introduced to rephrase the user's query into a clear standalone question using the original `user_message` and `chat_history`. This refined query, processed by a smaller LLM (`openai/gpt-4o-mini`), helps standardize user input, making sure the rewritten question contains full context of the conversation that might be omitted in the question itself, improving retrieval accuracy and response quality.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.49.07 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Example 2: HyDE (Hypothetical Document Embedding)**

When the [**HyDE**](basic-chat-agent-config.md#configuring-knowledge-for-the-chatbot) configuration is enabled, the workflow includes a step for generating a hypothetical document that could match the user’s query. A **String Template** is used to prompt the LLM to create a possible answer or passage for the given question. This synthesized content is then processed by the **LLM Completion** using a smaller model (`openai/gpt-4o-mini`). The output is a refined representation of the query, which helps guide the subsequent retrieval steps to locate the most relevant real documents in the knowledge base. By providing an initial synthesized document, HyDE aims to improve search precision, especially when direct matches might not be immediately apparent.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.55.41 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Example 3: Using Multiple Knowledge Bases with a Reranker**

When the configuration involves using multiple knowledge bases, the workflow adjusts to include several retrievers and a reranking step. Each retriever is connected to a different knowledge base, allowing the agent to search across various data sources. The retrievers independently process the user query and return a set of relevant documents from their respective knowledge bases.

To prioritize the most relevant results, a **Reranker** is applied. This component takes the results from the different retrievers and merges them into a single ranked list, ensuring that the top matches are prioritized for the final output. The reranker uses configurable weights and ranking logic to balance contributions from each knowledge base, enhancing the quality and relevance of the information retrieved.

The **Document String Reducer** then converts the merged and ranked results into a consolidated string format, making them ready for further processing. This approach allows the agent to tap into multiple sources while ensuring that the most pertinent information is surfaced for user queries.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 2.01.03 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Advanced Workflow Design Patterns

In this section, we explore some common design patterns that can be used to further customize workflows in various scenarios. These patterns offer flexibility and control, enabling users to tailor the behavior of chat and smart search agents to meet specific needs. By implementing these strategies, you can optimize how your AI agent processes, retrieves, and responds to user queries, creating a more dynamic and effective experience. Keep in mind that these are just a few examples—your creativity can take these ideas even further. The possibilities are limitless!

**Example 1. Metadata Filtering Pattern**

The metadata filtering pattern in the workflow view is designed to refine document retrieval based on specific conditions derived from user queries. A key part of this pattern is the **LLM Completion** node, which generates the filter condition dynamically.

First you need follow [instructions](../knowledge-base/advanced-settings/meta-data.md) to attach additional metadata fields to the knowledge table.

Then, create a workflow pattern with an additional LLM node connected after the user input node to analyze the user's input and identify references to particular metadata tags. This condition is then applied as a filter in subsequent retrieval steps, ensuring that only documents matching the specified criteria are returned. This approach enables a more targeted search, allowing the workflow to focus on highly relevant information, which improves the accuracy and relevance of the AI's responses.

In the example below, the system message within the LLM node might direct it to produce a filter string if the user's question mentions a specific source:

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 11.17.01 AM.png" alt="" width="563"><figcaption></figcaption></figure>

```
You analyze the user question, and if the user question mention anything about specific data source, then response a filter string:
Source LIKE '%{the_data_source}%'
Otherwise, response:
true
DON'T INCLUDE ANYTHING BEFORE OR AFTER YOUR RESPONSE FILTER STRING
```

Here is a more sophisticated case to create a nested condition for a financial analyst use case to filter on company ticker and quarter (read more [here](https://epsilla.com/blogs/ready-to-say-goodbye-to-data-chaos-discover-metadata-filtering-for-ai-agents-on-epsilla-cloud)):

```
Given the user question, extract the following key information and produce a single string with filter conditions accordingly based on instructions below:

1. If the user question mentions 1 company's name, produce filter string:

CompanyName = '{company_name}'
Example filter:

CompanyName = 'Apple'
2. If the user question mentions multiple companies' names instead of just 1 company, produce a filter string that uses OR to connect them, and add surrounding parentheses:

(CompanyName = '{company1_name}' OR CompanyName = '{company2_name}' OR ...)
Example filter:

(CompanyName = 'Nvidia' OR CompanyName = 'Meta')
3. If the user question mentions 1 quarter, like Q1, Q2, Q3, or Q4, produce filter string:

Time = '{the_quarter} 2024'
Example filter:

Time = 'Q1 2024'
4. If the user question mentions multiple quarters instead of just 1 quarter, produce a filter string that uses OR to connect them, and add surrounding parentheses:

(Time = '{the_quarter_1} 2024' OR Time = '{the_quarter_2} 2024' OR ...)
Example filter:

(Time = 'Q2 2024' OR Time = 'Q3 2024')
5. If ONLY ONE of the above rules is satisfied, then respond with that filter as the final result.

6. If more than one rule was satisfied in the above, generate a final filter that uses AND to concatenate them.

Example filter:

(CompanyName = 'Microsoft' OR CompanyName = 'Alphabet') AND Time = 'Q2 2024'
7. If no company or quarter is mentioned in the user question, then produce the response:

true
JUST RESPONSE THE FILTER CONDITION. DON'T INCLUDE ANYTHING BEFORE OR AFTER YOUR FILTER STRING.
```

&#x20;**Example 2. Knowledge Prioritization Pattern**

The knowledge prioritization pattern in the workflow view allows for direct integration of multiple retriever results into the LLM, without using a reranking mechanism. Instead of merging documents into a single list, this pattern feeds each set of retrieved knowledge directly to the LLM, letting it decide how to prioritize and weigh information from different sources. A **String Template** is used to guide the LLM on how to handle the inputs, such as always giving preference to knowledge from one source unless it lacks sufficient information, then falling back on the other. This approach offers a high degree of control over the AI's behavior, allowing for nuanced handling of knowledge sources. It is especially useful when specific sources of data should take precedence, enabling the agent to respond with a richer, more context-aware output based on a prioritized hierarchy of knowledge.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-20 at 1.16.34 PM.png" alt=""><figcaption></figcaption></figure>





Working in progress for more examples ...
