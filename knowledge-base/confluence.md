# Confluence

The **Confluence** data source in Epsilla enables users to connect and retrieve documents directly from Confluence spaces or specific pages. This type of data source is ideal for teams managing knowledge bases, project documentation, or internal resources in Confluence.

### Select Knowledge Base Type

Choose **Confluence** to continue.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.25.58 AM.png" alt="" width="325"><figcaption></figcaption></figure>

### **Knowledge Base Name**

Provide a **Knowledge Base Name**. A valid name should start with a letter or `_`, and can contain only letters, digits, underscores, and whitespaces. Example: `MyConfluenceDocs`.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.36.35 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Configure Confluence Connection**

Fill in the required fields to connect your Confluence instance:

* **Base URL**: The URL of your Confluence instance (e.g., `https://yourcompany.atlassian.net/wiki`).
* **Token**: A Confluence API token generated for your account. To access your Confluence API token, log in to your Atlassian account, navigate to your profile settings, and select "Create and manage API tokens" under the Security section; you can then generate a new API token there.
* **User Name**: The email associated with your Confluence account.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.38.12 AM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Load Data from Confluence**

There are two options for specifying the data to load from Confluence:

1. **Space Key**: Provide the key of the Confluence space to load all pages from that space.
2. **Page IDs**: Specify individual page IDs to load only selected pages. If page IDs provided, the space key will be ignored.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.39.53 AM.png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.41.08 AM.png" alt="" width="563"><figcaption></figcaption></figure>

To add multiple page IDs:

* Click **Add Multiple Page IDs**, enter the page IDs separated by new lines, and click **Add**.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.41.48 AM.png" alt="" width="375"><figcaption></figcaption></figure>

### Data Processing

Once the connection details are entered, click **Create**:

Epsilla will automatically process the pages. During this process, the platform loads, chunks, and embeds the documents into vectors for efficient retrieval. You can monitor the progress of data processing in real-time:

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.42.27 AM.png" alt="" width="563"><figcaption></figcaption></figure>

After the data is processed, the list of pages imported from **Confluence** will be visible in the **Loaded Pages** section. Pages that are ready for use will be marked as **Ready**, while those still processing will show a status of **Processing data**.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-24 at 11.43.31 AM.png" alt="" width="563"><figcaption></figcaption></figure>

You can update or edit your Confluence configuration by navigating to the **Data Sources** tab under your knowledge base.
