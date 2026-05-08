# Share Point

The **Share Point** data source in Epsilla allows users to connect their SharePoint environment to import documents into the knowledge base. This is useful for organizations that store a large number of documents in SharePoint, such as project files, reports, and collaborative documents.

### **Select Knowledge Base Type**

Choose **Share Point** as the data source type. Click **Continue** to proceed.

<figure><img src="../.gitbook/assets/choose sharepoint kb.png" alt="" width="333"><figcaption></figcaption></figure>

### **Knowledge Base Name**

Provide a **Knowledge Base Name** that will help you identify the data source. The name should start with a letter or an underscore (`_`) and can contain only letters, digits, underscores, and whitespaces, such as`MySharePointDocs`.

<figure><img src="../.gitbook/assets/sharepoint kb name.png" alt="" width="563"><figcaption></figcaption></figure>

### **Share Point Configuration**

To configure the SharePoint connection, you need the following details from your SharePoint environment:

* **Tenant ID**: Enter the Tenant ID of your SharePoint account.
* **Site ID**: Provide the Site ID of the SharePoint site that contains the documents you wish to load.
* **Client ID**: Enter the Client ID from the Azure AD app registration.
* **Client Secret**: Provide the Client Secret associated with the Client ID for authentication.

<figure><img src="../.gitbook/assets/share point config.png" alt="" width="563"><figcaption></figcaption></figure>

These credentials ensure a secure connection between Epsilla and your SharePoint environment.

### **Data Processing**

Once the required information is entered, click **Create** to start the knowledge base creation process. Epsilla will begin processing the documents from SharePoint. The progress of the data processing can be tracked.

<figure><img src="../.gitbook/assets/sharepoint kb creation progress.png" alt="" width="563"><figcaption></figcaption></figure>

After the data is processed, the list of documents imported from SharePoint will be visible in the **Loaded Files** section. Files that are ready for use will be marked as **Ready**, while those still processing will show a status of **Processing data**.&#x20;

<figure><img src="../.gitbook/assets/sharepoint process.png" alt="" width="563"><figcaption></figcaption></figure>

You can update or edit your SharePoint configuration by navigating to the **Data Sources** tab under your knowledge base.
