# Data Parsing

**Data Parsing** in Epsilla involves selecting a method to process and extract content from different types of data sources, such as PDFs, CSVs, or JSONL files.&#x20;

The **Data Parsing** option allows users to choose from various parsing modes, including **Auto**, which automatically detects the data format, or manual modes like **PDF**, **CSV**, and **JSONL**, depending on the source type. Additionally, advanced parsing options are available for processing tables and charts.

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 4.12.37 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### When to use Auto

In most cases, the default Auto mode is sufficient. It automatically detects the data file format and leverages different types of file loaders accordingly. If your data source contains multiple file types (such as PDF, DOC, TXT, JSON, CSV, HTML, etc.), Auto is your best choice.

### When to use PDF, CSV, or JSONL

If you only have one type of file in your knowledge base, you can optionally use PDF, CSV, or JSONL as your parsing option.

### When to use Advanced Parsing with Tables/Charts

This option is currently available only for the Enterprise tier. It provides superior data extraction accuracy using an industry-leading Large Vision Language Model (VLM) technique provided by [CambioML](https://www.cambioml.com/). At present, we support only PDF files. This option can accurately extract text, nested tables, and charts from PDF files in any layout. Read more in our [white paper](https://epsilla.com/AnyParser\_Epsilla\_Whitepaper.pdf#zoom=100%).

[Talk to us](https://epsilla-ai.larksuite.com/scheduler/4aca8159d1224454) if you want to use this technology without an Enterprise tier to test it out. We'd love to enable it for you and support your use case!
