# RAG with Qdrant Vector Store Workflow

This workflow implements a **Retrieval-Augmented Generation (RAG) chatbot** using n8n, Ollama embeddings, and Qdrant as the vector store.  

---

## 🎯 Purpose
Enable users to **chat with uploaded documents** by:  
- Ingesting PDFs into a semantic database (Qdrant)  
- Creating embeddings using Ollama  
- Performing RAG queries to answer questions  
- Maintaining conversation context with memory  

Designed for teams or users who want a **self-hosted, document-aware AI chatbot**.

---

## ⚙️ How It Works
1. **Form Submission** → Users upload a file (PDF only).  
2. **Default Data Loader** → Reads the uploaded file.  
3. **Text Splitter** → Splits document into chunks for semantic search.  
4. **Embeddings (Ollama)** → Converts chunks into vector embeddings.  
5. **Qdrant Vector Store** → Stores embeddings for retrieval.  
6. **Chat Trigger** → Listens for incoming chat messages.  
7. **AI Agent** → Queries Qdrant and generates context-aware responses.  
8. **Memory Buffer** → Maintains conversation context.  
9. **LLM (Ollama Chat Model)** → Generates human-readable answers.  

---

## 🔑 Requirements
- n8n instance  
- Qdrant (self-hosted or cloud) with a collection named `rag_collection`  
- Ollama Local Url for embeddings and chat model  

---

## 🚀 How to Use
1. Import `RAG with Qdrant Vector Store.json` into n8n.  
2. Set up credentials:  
   - **Qdrant** → API key and collection `rag_collection`  
   - **Ollama** → URL key for embeddings and chat  
3. Adjust chunk size / overlap in the **Recursive Character Text Splitter** node if needed.  
4. Upload a PDF via the form node to ingest data.  
5. Start chatting using the **chat trigger**; the AI will respond using context retrieved from Qdrant.  

---

## ⚙️ Notes
- **Memory Buffer**: Keeps recent messages for coherent conversation.  
- **Embeddings**: Ollama embeddings are used for semantic search. You can swap in another provider if desired.  
