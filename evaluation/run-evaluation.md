# Run Evaluation

### **Choose the Evaluation To Run**

Choose which evaluation to run from the evaluations list.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.39.49 AM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.26.35 AM.png" alt=""><figcaption></figcaption></figure>

**Choose the AI Agent(s) to Evaluate**

Select the AI agent(s) that you wish to evaluate from the dropdown menu.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.33.55 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* You can evaluate different versions of AI agents. For example, you might compare the performance of a base agent with an advanced or fine-tuned version. The dropdown menu will list available agents for the selected application.
* Multiple agents can be compared across the same evaluation for consistency and improvement tracking.

### **Run the Evaluation:**

Click the **Run Evaluation** button.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.34.03 AM.png" alt="" width="186"><figcaption></figcaption></figure>

* Epsilla's evaluation engine will process the questions and instruct the agent to generate answers.
* The system will visualize the agent’s process, showing the data or "chunks" retrieved for each question and the generated answer.

### Key Metrics for Evaluation

Epsilla provides several key metrics to measure agent performance:

* **Answer Correctness:** Assesses how well the agent's responses match the expected answers.
* **Answer Relevance:** Measures the degree to which the agent's response is related to the question asked.
* **Answer Faithfulness:** Ensures that the response is grounded in retrieved or generated content, preventing fabricated or "hallucinated" answers.
* **Context Precision:** Evaluates how precisely the agent retrieves chunks required to answer the question.
* **Context Coverage:** Determines if the agent retrieves all relevant chunks to provide the expected answer.

### Viewing and Analyzing Results

As the evaluation runs, you will be able to see the agent retrieving multiple chunks of data for each question. The system will provide real-time feedback on how well the agent is performing across the key metrics.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.34.35 AM.png" alt=""><figcaption></figcaption></figure>

After completion, results are shown in a detailed table, including the questions, expected answers, actual agent responses, and the scores for each metric. These results help identify areas where the agent excels and areas where further optimization is needed.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.47.32 AM.png" alt=""><figcaption></figcaption></figure>

Epsilla provides tools to visualize the evaluation results. Clicking on the **Analyze Evaluation Result** button opens a dashboard that shows a summary of the agent’s performance across the key metrics.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.35.47 AM.png" alt="" width="563"><figcaption></figcaption></figure>

Graphs and charts allow you to quickly identify patterns, such as high relevance but low faithfulness, helping you pinpoint specific areas for further training or fine-tuning.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.35.59 AM.png" alt=""><figcaption></figcaption></figure>

The results of an evaluation can be exported for further analysis or reporting. Click the **Export Result** button to download the evaluation data in spreadsheet. This feature is especially useful for sharing results with stakeholders or integrating them into a broader performance review process.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.35.39 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### Running and Comparing Multiple AI Agents for Performance Optimization

Running and comparing multiple AI agents within Epsilla allows users to evaluate different versions or configurations of agents under the same set of conditions. By selecting different agents from the dropdown and running evaluations side by side, users can generate comparative metrics across key performance areas like answer correctness, relevance, faithfulness, and precision.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.52.35 AM.png" alt="" width="563"><figcaption></figcaption></figure>

Once the evaluation completes, the system provides visual comparisons, such as bar charts, that allow users to quickly identify which agent excels in particular areas. This comparative analysis is essential for optimizing agents, as it highlights strengths and areas for improvement across versions, ensuring continuous enhancement of the AI's capabilities.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 12.52.26 AM.png" alt="" width="375"><figcaption></figcaption></figure>

### Continuous Agent Improvement

The evaluation process in Epsilla is designed to be iterative. By running regular evaluations, you can continually improve the performance of AI agents. This helps ensure that agents are always up to date with the latest data, optimizations, and business needs. The platform also supports the integration of new datasets or scenarios for even more customized evaluations.
