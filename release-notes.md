# Release Notes

### 📦 March 2025 – Major Test Infrastructure & Pipeline Enhancements

#### ✅ Testing & CI/CD

* Upgraded the CI pipeline for better automation, faster feedback, and error visibility.
* Introduced and expanded `pytest` framework for ETL testing.
* Added test coverage across shared libraries and core modules.

#### 🔄 Internal Refactors

* Refactored shared libraries and internal tools for better modularity.
* Upgraded ETL Dockerfile to Python 3.11.11-slim for improved performance.

#### 🧩 Agent & Template Enhancements

* Enhanced agent backend with versioning, naming conventions, and templated auto-instantiation.
* Improved auto agent pipeline and prefix handling logic.

#### ⚙️ Chat System Improvements

* Added support for chat deletion and improved chat endpoint stability.
* Minor typo corrections and internal cleanup of chat code.

***

### 📦 February 2025 – Jira Integration, Query Tooling & Voice Support

#### 📋 Jira & Workflow Integration

* Enabled Jira ticket generation via API and Google Forms integration for workflow triggers.

#### 🧰 Query & Retrieval

* Introduced Cypher query tools for graph-based retrieval.
* Added domain-specific query support for customized search experiences.

#### 🎙️ Voice & Input

* Enabled microphone and voice input within embedded iframes.
* Production-ready transcription integrated for voice-to-text.

#### 🔧 Package & Docker Enhancements

* Updated Dockerfiles and dependencies across modules for security and performance.

***

### 📦 January 2025 – Chat System Refactor & WhatsApp Integration

#### 💬 Chat & Conversation Overhaul

* Migrated chat system to DynamoDB, supporting full conversation tracking and querying.
* Improved `conversation_id` handling for user-level context tracking.

#### 📲 Messaging & Integrations

* Integrated WhatsApp as a communication channel.
* Improved MongoDB connection and DeepSeek model support.

#### 📚 Multimodal Support

* Added image reading and basic PDF metadata extraction.

***

### 📦 December 2024 – Jira Delta Sync & Confluence Connector

#### 🔁 Jira Enhancements

* Improved Jira delta sync logic with enhanced JQL parsing and debugging tools.

#### 📓 Confluence Integration

* Built robust HTML content extractor and metadata sync for Confluence.
* Enhanced ingestion and cleanup tools.

#### 🧹 Logging & Cleanup

* Reduced excessive logs, improved log clarity, and optimized pipeline stringification.

***

### 📦 November 2024 – Hypothetical Questions & Retriever Upgrades

#### 🔍 Search & Retrieval

* Added support for hypothetical questions in RAG.
* Introduced batch semantic retriever and advanced Cypher query handling.

#### 🔧 Connector & ETL Improvements

* Upgraded connectors for Google Cloud, Azure, MongoDB, and Box.
* Improved ETL logic for multimodal and multifile document support.

***

### 📦 October 2024 – RAG Tools & Graph-Based Extensions

#### 🌐 RAG Enhancements

* Integrated semantic retrievers, hypothetical rephrasing, and `rag_tool` foundations.

#### 🌉 Graph RAG

* Enabled graph traversal using Cypher and TigerGraph integration.
* Deployed graph-based query pattern tools.

#### 🕸️ Dynamic Web Loading

* Improved website crawling using FireCrawl and bot-avoidance mechanisms.

***

### 📦 September 2024 – Quota Control, Evaluation Engine, and Chatbot Workflow

#### 📊 Usage Control & Billing

* Enforced subscription-based limits for file uploads and applications.
* Enhanced billing UI with upgrade prompts and usage tracking.

#### 📈 Evaluation Engine (Beta)

* Launched evaluation interface with metrics like ROUGE and token overlap.
* Users can configure, run, and view evaluation results via dashboard.

#### 🤖 Workflow Support

* Released chatbot workflow config UI with prompt templating and zero-knowledge search.
* Redesigned chat config with new logic layers and routing.

***

### 📦 August 2024 – Preview Chatbots, Hypothetical Search & Google Drive Support

#### 🧪 Preview & Publishing

* Enabled chatbot preview before publishing, including summary and sample question customization.

#### 🔎 Retrieval Enhancements

* UI-configurable hypothetical questions for improved RAG.
* Runtime knowledge base switching support.

#### ☁️ Cloud & Integration

* Full support for Google Drive and Google Cloud Storage connectors.
* Added OAuth-based Notion and Outlook integrations.

***

### 📦 July 2024 – Application Builder Foundations & LLM Integrations

#### 🧱 App Builder

* Step-by-step app creation flow with chat, search, and evaluation modes.
* Enhanced drag-and-drop upload and real-time previews.

#### 🔨 Project Management

* Enabled project-level access controls, tiering, and form validations.

#### 🧠 Model Integrations

* Added Azure OpenAI and Gemini support.
* Internal tooling for rerankers and graph traversal logic.

***

### 📦 June 2024 – Custom UI, Web Widget & GPT-4o Upgrade

#### 🎨 UI Branding & Embeds

* Released `epsilla.js` for website embedding.
* Custom logos, markdown, LaTeX, and theme controls supported.

#### 🤖 GPT-4o Support

* Upgraded default LLM to GPT-4o for speed and performance.

#### 📡 Sync & Web Retrieval

* Improved web content syncing and chunking logic.
* Added dynamic knowledge refresh options.

***

### 📦 May 2024 – Debug Tools & File-Level Enhancements

#### 🧪 Workflow Debugging

* Introduced debug mode for apps with real-time render visualization.
* Stored debug sessions for replay and analysis.

#### 📁 File-Level RAG

* Per-file sync tracking and metadata display.
* Special character support in file names and paths.

#### ✨ UI Improvements

* Opacity control, improved iframe embedding, table rendering in markdown.

***

### 📦 April 2024 – Chat Sharing, Financial Modules & File Enhancements

#### 📤 App Sharing

* Enabled public sharing of chatbot messages and apps via URL.

#### 💰 Financial RAG

* Added financial-specific prompt templates and timeout settings.
* Integrated CambioML for custom vertical workflows.

#### 📁 File UX

* Better file chunking, preview rendering, and filename validation.

***

### 📦 March 2024 – Smart Search, Voice Input & Live Knowledge Streaming

#### 🔍 Smart Search

* Added dynamic stream of knowledge base during query resolution.
* Real-time updates to rephrasing logic and query adaptation.

#### 🎙️ Voice Input

* Experimental voice transcription and multi-modal UX introduced.

#### 🖼️ UI Polishing

* Markdown enhancements, input resizing, responsive layout tuning.

