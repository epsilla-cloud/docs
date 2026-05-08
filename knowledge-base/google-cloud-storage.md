# Google Cloud Storage

The **Google Cloud Storage (GCS)** data source in Epsilla allows users to seamlessly connect their GCS bucket to manage documents stored in the cloud. This type of data source is ideal for adding dynamic or shared content, such as PDFs, images, or structured files, to the knowledge base for retrieval purposes.

### **Select Knowledge Base Type**

Choose **Google Cloud Storage** to continue.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 5.37.53 PM.png" alt=""><figcaption></figcaption></figure>

### **Knowledge Base Name**

Provide a Knowledge Base Name. A valid name should start with a letter or '\_', and can contain only letters, digits, underscores, and whitespaces (e.g., `MyGCSDocs`).

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 5.40.00 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Configure GCS Connection**

Provide the required details to connect to your GCS bucket:

* **Service Account Credential**: Paste the content from your GCP `credentials.json` file.
* **Bucket**: Specify the name of your GCS bucket (e.g., `epsilla-gcs-demo`).
* **Prefix** _(Optional)_: Enter the folder path within the bucket if you want to sync specific folders. Leave blank to sync the entire bucket.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 5.39.04 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Data Processing**

Once the required information is entered, click **Create** to start the knowledge base creation process. Epsilla will automatically process the files (under the hood, Epsilla will load the files, chunk them, and embed them into vectors).

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 5.40.21 PM.png" alt="" width="523"><figcaption></figcaption></figure>

After the data is processed, the list of documents imported from GCS will be visible in the **Loaded Files** section. Files that are ready for use will be marked as **Ready**, while those still processing will show a status of **Processing data**.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-12-02 at 5.40.47 PM.png" alt="" width="563"><figcaption></figcaption></figure>

You can update or edit your Google Cloud Storage configuration by navigating to the **Data Sources** tab under your knowledge base.
