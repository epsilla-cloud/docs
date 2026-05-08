# Data Chunking

**Data Chunking** in Epsilla involves selecting a method to divide data into smaller, manageable segments for efficient processing and retrieval. Due to the context window limitation of Large Language Models, we cannot pass the entire knowledge base to the LLM during generation. Therefore, we need to chunk the data into smaller pieces, create a semantic index on top of them (via embedding), and retrieve the most relevant pieces of information during each LLM generation.

The Data Chunking option allows users to choose from various chunking modes.

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 4.40.10 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### Split by Sentences

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 5.56.44 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The "Split by sentence" option in data chunking involves breaking the text into chunks that respect natural sentence boundaries, ensuring that each chunk contains several complete sentences rather than incomplete sentence cut in the middle.

The chunk size controls the maximum number of characters in a chunk, while the chunk overlap determines how many characters will overlap between chunks.

### Markdown Splitter

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 5.59.26 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The "Markdown Splitter" breaks down Markdown documents into smaller chunks based on different structural elements, such as headings and paragraphs. This allows for a more organized and efficient processing of the content, making it suitable for indexing, querying, and further transformations.

The chunk size controls the maximum number of characters in a chunk, while the chunk overlap determines how many characters will overlap between chunks.

### Recursive Splitting

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 6.08.00 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The "Recursive Splitting" option in data chunking involves iteratively breaking the text into smaller segments using predefined characters or separators, ensuring each chunk remains consistent in size and context.

The chunk size controls the maximum number of characters in a chunk, while the chunk overlap determines how many characters will overlap between chunks.

### Smart Chunking

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-04 at 6.10.33 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The "Smart Chunking" option is Epsilla's proprietary chunking method for Markdown documents with a hierarchical structure (titles, subtitles, etc.). It balances chunk cohesiveness by attempting to keep the same section within one chunk, unless the chunk size becomes too large. Additionally, it attaches the hierarchical titles of parent sections to each chunk to maintain context. It is best used in combination with [Advanced Parsing with Tables/Charts](data-parsing.md#when-to-use-advanced-parsing-with-tables-charts) to achieve optimal data processing performance.
