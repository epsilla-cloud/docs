# Notion

The **Notion** data source in Epsilla enables users to connect to their Notion workspace, allowing them to load Notion databases (DB) or pages into the knowledge base. This is particularly useful for pulling structured content like notes, tasks, and project documentation directly from Notion.

### **Select Knowledge Base Type**

Select **Notion** as the data source type. Click **Continue** to proceed.

<figure><img src="../.gitbook/assets/choose notion data source.png" alt="" width="330"><figcaption></figcaption></figure>

### **Knowledge Base Name**

Provide a **Knowledge Base Name** that will help identify the data source. The name should begin with a letter or an underscore (`_`) and can contain only letters, digits, underscores, and whitespaces. For example, enter `MyNotionDocs`.

<figure><img src="../.gitbook/assets/notion kb name.png" alt="" width="563"><figcaption></figcaption></figure>

### **Notion Authentication**

**Token**: Provide your Notion Integration Token to allow Epsilla to access your Notion workspace. You can generate the token by setting up a Notion integration and using the token provided in Notion’s API settings. [Instructions and examples](notion.md#notion-integration-instructions) are at the end.

<figure><img src="../.gitbook/assets/notion token.png" alt="" width="563"><figcaption></figcaption></figure>

After entering the token, you can choose to import either **Database** or **Pages**.

### **Load from Notion Databases**

To import a database, select **Database**. Enter the **Database ID** from Notion that you wish to connect. You can find the Database ID in the URL of your Notion page.

<figure><img src="../.gitbook/assets/notiont add db id.png" alt="" width="563"><figcaption></figcaption></figure>

### **Load from Notion Pages**

To import individual pages, select **Pages**. Enter the **Page IDs** of the Notion pages you wish to load.

You can add a **Single Page ID.**

<figure><img src="../.gitbook/assets/notion add single page id.png" alt="" width="563"><figcaption></figcaption></figure>

Or you can choose to add **Multiple Page IDs** at once by separating them with new lines.

<figure><img src="../.gitbook/assets/notion add multi page ids.png" alt="" width="375"><figcaption></figcaption></figure>

### **Data Processing**

Once you have entered the necessary information (Token and Database/Page IDs), click **Create** to initiate the knowledge base creation. Epsilla will automatically process the content, importing it into the knowledge base.&#x20;

<figure><img src="../.gitbook/assets/notion creation progress.png" alt="" width="563"><figcaption></figcaption></figure>

After the data is processed, you can view the list of loaded Notion documents (either database entries or pages) in the **Loaded Files** section. Files that are ready for use will be marked as **Ready**, while those still processing will show a status of **Processing data**.

<figure><img src="../.gitbook/assets/notion process.png" alt="" width="563"><figcaption></figcaption></figure>

You can add additional pages or databases later by navigating to the **Data Sources** tab of your knowledge base.

### Notion Integration Instructions

This guide provides step-by-step instructions on creating an internal-use Notion integration, retrieving the integration token, and connecting it to your Notion pages or databases. This integration is for internal use only and will allow you to securely automate and interact with your Notion workspace.

**Create a New Integration in Notion**

*   **Navigate to Integrations**:

    Go to `https://notion.so/profile/integrations`. You will see a section called **Integrations**.
*   **Create a New Integration**:

    Click on the **New integration** button under "Integrations." Fill in any required details for your integration, such as integration name.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-15 at 12.15.57 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Retrieve the Internal Integration Secret (Token)**

*   **Locate your Integration Token**:

    Once you’ve created the integration, you will be provided with an **Internal Integration Secret**. The token is essential for authenticating your API requests to Notion.
*   **Copy the Secret**:

    Copy this token by clicking on **Show** (as seen in the screenshot) and saving it securely.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-15 at 12.44.31 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Connect Your Integration to a Notion Database/Page**

*   **Find the Database/Page You Want to Connect**:

    Open the desired database or page in Notion that you want the integration to interact with. In the page's menu (right-hand side), select **Connections** and click **Connect to**.
*   **Select Your Integration**:

    From the list of available integrations, choose the one you just created (e.g., "my-notion-test"). This will establish a connection between your Notion page or database and your newly created integration.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-15 at 12.16.37 AM.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2024-10-15 at 12.16.49 AM.png" alt="" width="273"><figcaption></figcaption></figure>

**Find the Notion Page ID**

When you're on the desired Notion page, check the URL in your browser. The page ID is the string of characters after the last dash (`-`) in the URL. For example, in the screenshot: `doc1-1185a837ddfb4b74bfff9fc7b5`, the page ID is `1185a837ddfb4b74bfff9fc7b5`.
