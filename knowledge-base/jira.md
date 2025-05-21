# Jira

The **Jira** data source in Epsilla allows users to connect and retrieve issues directly from their Jira projects or specific issues. This type of data source is ideal for managing tickets, project progress, and collaboration data stored in **Jira**.

### Select Knowledge Base Type

Choose **Jira** to continue.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.05.19 PM.png" alt="" width="325"><figcaption></figcaption></figure>

### Knowledge Base Name

Provide a **Knowledge Base Name**. A valid name should start with a letter or `_`, and can contain only letters, digits, underscores, and whitespaces. Example: `MyJiraDocs`.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.05.49 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Configure Jira Connection

Fill in the required fields to connect your Jira instance:

1. **Base URL**: The URL of your Jira instance (e.g., `https://yourcompany.atlassian.net`).
2. **Token**: A Jira API token generated for your account. To access your Jira API token:
   * Log in to your Atlassian account.
   * Navigate to your profile settings.
   * Select **"Create and manage API tokens"** under the Security section.
   * Generate a new API token and copy it.
3. **User Name**: The email address associated with your Jira account.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.07.03 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Load Data from Jira

There are two options for specifying the data to load from **Jira**:

1. **Project Key**: Provide the key of the Jira project to load all issues from that project.
2. **Issue Keys**: Specify individual issue keys to load selected tickets. If issue keys are provided, the project key will be ignored.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.07.36 PM.png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.07.55 PM.png" alt="" width="563"><figcaption></figcaption></figure>

To add multiple issue keys:

* Click **Add Multiple Issue Keys**, enter the keys separated by new lines, and click **Add**.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.08.20 PM.png" alt="" width="375"><figcaption></figcaption></figure>

### Data Processing

Once the connection details are entered, click **Create**:

Epsilla will automatically process the tickets. During this process, the platform loads, chunks, and embeds the documents into vectors for efficient retrieval. You can monitor the progress of data processing in real-time:

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.08.40 PM.png" alt="" width="563"><figcaption></figcaption></figure>

After the data is processed, the list of pages imported from **Jira** will be visible in the **Loaded Issues** section. Tickets that are ready for use will be marked as **Ready**, while those still processing will show a status of **Processing data**.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 12.09.20 PM.png" alt="" width="563"><figcaption></figcaption></figure>

You can update or edit your Jira configuration by navigating to the **Data Sources** tab under your knowledge base.
