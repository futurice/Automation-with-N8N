# Slack AI Agent Chatbot Workflow

This workflow creates an **AI-powered assistant inside Slack** using n8n, LLMs, and a document retrieval system.  

---

## 🎯 Purpose
The chatbot helps users quickly access knowledge and documentation directly in Slack.  

It is designed to:  
- Answer queries about company procedures and documents  
- Retrieve information from a **Qdrant vector database** (via RAG – Retrieval Augmented Generation)  
- Maintain conversation context with memory  

---

## ⚙️ How It Works
1. **Slack Trigger** → Listens for mentions (`@bot`) in a Slack channel.  
2. **AI Agent** → Powered by an LLM (e.g., Ollama, Azure OpenAI).  
3. **RAG (Qdrant Vector Store)** → Retrieves relevant information from company documents.  
4. **Memory Buffer** → Keeps track of the last few messages for context.  
5. **Slack Response** → Sends a concise, cited, and formatted reply back into the thread.  

---

## 🔑 Requirements
- n8n instance  
- Slack App & OAuth credentials  
- Qdrant (cloud or self-hosted) for storing embeddings  
- Google Drive (optional) for sourcing documents  
- Ollama / Azure OpenAI (or any LLM API)  

---

## 🚀 How to Use
1. Import `Slack AI Agent Chatbot.json` into n8n  
2. Set up credentials:  
   - **Slack** → App + OAuth setup  
   - **Qdrant** → API key and collection name  
   - **LLM (Ollama / OpenAI / Azure OpenAI)**  
   - **Google Drive** (if loading documents automatically)  
3. Update the workflow with your Qdrant collection name & Slack channel ID  
4. Deploy and start chatting with your AI assistant in Slack 🎉  
