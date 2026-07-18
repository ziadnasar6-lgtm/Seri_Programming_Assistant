# Seri_Programming_Assistant

# AI_programming_Seri_v1 🤖💻

AI_programming_Seri_v1 is an autonomous, multi-agent AI assistant built on n8n designed to automate software development tasks, manage files, and interact with cloud workspaces. 

The system leverages a central AI Agent triggered via **Telegram**, connected to local **Ollama** models, and backed by a complete **RAG (Retrieval-Augmented Generation)** pipeline using **Pinecone** and **Google Drive**.

---

## 🛠️ Tech Stack & Integrations

*   **Orchestration Engine:** ![n8n](https://img.shields.io/badge/n8n-FF6C37?style=flat&logo=n8n&logoColor=white)
*   **LLM & Embeddings:** ![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat&logo=ollama&logoColor=white) (Local Intelligence)
*   **Vector Database (RAG):** ![Pinecone](https://img.shields.io/badge/Pinecone-1a1a1a?style=flat&logoColor=white) 
*   **User Interface:** ![Telegram](https://img.shields.io/badge/Telegram-26A5E4?style=flat&logo=telegram&logoColor=white) (ChatOps Bot)
*   **Cloud Workspace:** ![Google Drive](https://img.shields.io/badge/Google%20Drive-4285F4?style=flat&logo=googledrive&logoColor=white) (File Source & Syncing)
*   **Development Tools:** ![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white) & ![SerpAPI](https://img.shields.io/badge/SerpAPI-4285F4?style=flat&logo=google&logoColor=white) (Web & Repository Search)

---

## 📐 Architecture Breakdown

The workflow is meticulously organized into three main functional layers:

### 1. 🔴 Main Agent Layer (Chat UI)
*   **Trigger:** Activated dynamically when a chat message or command is received via the **Telegram Trigger** node.
*   **Core Intelligence:** An **AI Agent** routed to an **Ollama Chat Model** utilizing **Simple Memory (Window)** to remember context and chat history.
*   **Output:** Replies back asynchronously to the user through the **Telegram Send Message** node.

### 2. 🟢 Question & Code Search Tool
A modular sub-agent (`Question agent`) tailored for technical investigation:
*   Queries the web dynamically using **SerpAPI (Google Search)**.
*   Interfaces with the **GitHub API** (`Get a repository`) to pull public/private code samples and repositories for analysis.

### 3. 🟤 Backend & RAG Pipeline (Workspace Integration)
A specialized sub-workflow designed to inject context into the AI:
*   **Dynamic Document Syncing:** Automatically triggers upon modifications in a **Google Drive** folder (`Google Drive Trigger` & `When looking 'Execute workflow'`).
*   **Data Processing:** Searches files/folders, downloads files (`Download File`), and runs custom JavaScript scripts (`Code Node`) to parse and structure contents.
*   **Vector Vector Store (Pinecone):** Converts codebases and documents into semantic vector embeddings using an Ollama embedding model, then inserts them into **Pinecone Vector Store** via the **Default Data Loader**.
*   **Semantic Search:** Allows the Main Agent to query the vector space (`Answer questions with a vector store`) to retrieve ground-truth codebase information instantly.

---

## 🚀 Key Features

*   **ChatOps for Programming:** Command your autonomous AI developer agent straight from your Telegram app.
*   **Full-Scale Code RAG:** Automatically vectorizes and stores your project files from Google Drive to answer architecture or debugging questions precisely.
*   **Seamless GitHub Integration:** Fetches repository structures and file states natively during the flow execution.
*   **Private AI Context:** Combines the security of local models (Ollama) with the scalability of cloud vector data stores (Pinecone).

---

## 🔧 Installation & Setup

1. Clone or export the workflow JSON from this repository.
2. Import the JSON canvas into your **n8n** instance.
3. Configure the following integrations and credentials within n8n:
   * **Telegram Bot Token** (via BotFather).
   * **Ollama Connection Host** (ensure your local instance allows external CORS/API calls if n8n is hosted).
   * **Google Drive OAuth2** credentials.
   * **Pinecone API Key** and Environment setup.
   * **GitHub Credentials / Personal Access Token**.
   * **SerpAPI Key** for fallback web searching.
4. Set up the dynamic paths for your target Google Drive folder.
5. Hit **Publish** to put the agent online.

---

## 👤 Author

*   **Ziad Nassar** - [GitHub Profile](https://github.com/ziadnassar6-lgtm)
