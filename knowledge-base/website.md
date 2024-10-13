# Website

The **Website** data source in Epsilla allows users to import and manage content directly from webpages, making it ideal for dynamic or continuously updated information. This type of data source is optimal for retrieving data from websites, blogs, and other web-based platforms into the knowledge base.

### **Select Knowledge Base Type**

To begin, choose **Website** as the data source to load content from webpages.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.02.17 AM.png" alt="" width="375"><figcaption></figcaption></figure>

Click **Continue** to proceed.

### **Knowledge Base Name**

Provide a **Knowledge Base Name**. The name should begin with a letter or an underscore (`_`), and can contain only letters, digits, underscores, and whitespaces. Enter your desired name in the input box, such as `MyWebsiteKnowledge`.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.02.49 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Add Webpage URLs**

In the **Webpage URLs** section, input the publicly accessible URLs you want to extract data from.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.03.02 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* The URLs must start with `http://` or `https://`.
* You can add a **Single Webpage** manually, **Crawl** a webpage for subpages, or add multiple webpages at once.

For example, you can manually enter:

```arduino
https://epsilla-inc.gitbook.io/epsilladb
```

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.03.32 AM.png" alt="" width="563"><figcaption></figcaption></figure>

To **crawl a webpage**, click the **Crawl webpage** button. In the dialogue that appears:

* Input the base URL, such as `https://epsilla-inc.gitbook.io/`.
* Set the **Max number of pages** to crawl (e.g., 100).

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.03.43 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* Click **Search** to locate subpages. A list of subpages will be displayed.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.04.03 AM.png" alt="" width="563"><figcaption></figcaption></figure>

* Select the pages you want to include in the knowledge base and click **Add**.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.04.11 AM.png" alt="" width="563"><figcaption></figcaption></figure>

You can also use the **Add multiple webpages** option to input multiple URLs at once, separated by new lines.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.05.07 AM.png" alt="" width="563"><figcaption></figcaption></figure>

**Data Processing**

Once you've added the desired URLs, click **Create** to begin processing the data.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.11.15 AM.png" alt="" width="563"><figcaption></figcaption></figure>

Epsilla will automatically retrieve the content from the pages, chunk it into manageable pieces, and embed it into vectors. You can monitor the progress during this step.

<figure><img src="../.gitbook/assets/Screenshot 2024-10-13 at 1.11.38 AM.png" alt="" width="563"><figcaption></figcaption></figure>

You can inspect the processed data (chunks) at the [**Data Storage**](data-storage.md) tab.[\
](https://epsilla-inc.gitbook.io/epsilladb/knowledge-base)
