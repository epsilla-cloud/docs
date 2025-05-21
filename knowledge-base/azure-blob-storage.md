# Azure Blob Storage

The **Azure Blob Storage** data source in Epsilla enables users to connect to an Azure Blob Storage container and manage documents for their knowledge base. This integration is perfect for handling documents stored in cloud environments, such as PDFs, Word documents, images, or spreadsheets, for retrieval purposes.

### Select Knowledge Base Type

Choose **Azure Blob Storage** to proceed.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 6.05.01 PM.png" alt=""><figcaption></figcaption></figure>

### Knowledge Base Name

Provide a **Knowledge Base Name**. A valid name must start with a letter or '\_', and it can contain only letters, digits, underscores, and whitespaces. Example: `MyABSDocs`.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 6.06.08 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Configure Azure Blob Storage Connection

Input the following details to connect your Azure Blob Storage container:

1. **Storage Account Name**: Provide the name of your Azure Blob Storage account (e.g., `epsillablobstaging`).
2. **Storage Access Key**: Enter the access key associated with your Azure Blob Storage account.
3. **Bucket | Container Name**: Specify the container name where your documents are stored (e.g., `epsilla`).
4. **Prefix** _(Optional)_: If you want to focus on a specific folder or path within the container, enter it here. Leave it blank to use the bucket root.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 6.07.08 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Data Processing

Once the connection details are entered, click **Create**:

Epsilla will automatically process the container files. During this process, the platform loads, chunks, and embeds the documents into vectors for efficient retrieval. You can monitor the progress of data processing in real-time:

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 6.07.23 PM.png" alt="" width="524"><figcaption></figcaption></figure>

After the data is processed, the list of documents imported from the container will be visible in the **Loaded Files** section. Files that are ready for use will be marked as **Ready**, while those still processing will show a status of **Processing data**.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 6.07.48 PM.png" alt="" width="563"><figcaption></figcaption></figure>

You can update or edit your Azure Blob Storage configuration by navigating to the **Data Sources** tab under your knowledge base.
