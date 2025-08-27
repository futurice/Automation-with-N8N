# n8n Workflows Collection

Welcome to the **n8n Workflows Collection** 🚀  
This repository provides ready-to-use workflows for [n8n](https://n8n.io/), an open-source workflow automation tool. The goal is to help teams streamline their processes, integrate tools, and build AI-powered automations with minimal effort.

---

## 🌟 What is n8n?
[n8n](https://n8n.io/) is a **workflow automation platform** that allows you to connect different apps and services using a low-code approach.  
- Automate repetitive tasks  
- Connect APIs and Services  
- Integrate AI into workflows  
- Run on your own server (self-hosted) or use the cloud version.

---

## ✅ Benefits of Using These Workflows
- **Prebuilt Automations** → Save time with workflows designed for real use cases  
- **Customizable** → Modify nodes, credentials, or logic to suit your needs  
- **Scalable** → From simple tasks to AI-driven workflows  

---

## 📂 Repository Structure


- **Asana_Automation/**  
  Automates Asana projects and tasks with AI. Includes a **chatbot UI (`chatbot.html`)** for interaction.  

- **Slack_AI_Agent_Chatbot/**  
  Creates an AI chatbot inside Slack that connects to your company’s knowledge base and answers queries.

- **RAG_with_Qdrant_VectorStore/** 
  Allows you to ingest documents, generate embeddings, and chat with your data using an AI agent.

- **docker-compose.yml**  
  Configuration to run n8n + Postgres locally with Docker.  

Each folder includes:  
- `workflow.json` → The actual n8n workflow export  
- `README.md` → Documentation explaining the workflow’s purpose and setup  

---

## 📖 N8N Documentation & Resources
- n8n Docs: [https://docs.n8n.io](https://docs.n8n.io)  
- Community: [https://community.n8n.io](https://community.n8n.io)  

---

# Running n8n Locally with Docker

A step-by-step guide to run **n8n** locally using Docker Compose, import the provided workflows, and run the Asana chatbot frontend.

---

## 🐳 Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed  
- [Docker Compose](https://docs.docker.com/compose/install/) installed  
- A terminal/command prompt  
- (Optional) Python or http-server to serve static files for the chatbot UI  

---

## 📦 Repository Contents

- `docker-compose.yml` — runs Postgres (with pgvector) and n8n  
- `Asana_Automation/Asana_Automation.json` — Asana workflow export  
- `Asana_Automation/chatbot.html` — lightweight frontend that sends messages to an n8n webhook  
- `Slack_AI_Agent_Chatbot/` — Slack AI Agent workflow export  
- `RAG_with_Qdrant_VectorStore/` — RAG workflow using Qdrant vector store for document ingestion, embeddings, and AI-assisted chat

---

## ⚙️ Docker Compose Configuration

This repository already contains a `docker-compose.yml` file with the required parameters.

---
## 🗝️ Parameter Variables

You can configure n8n and its database either by using a `.env` file or directly in the `docker-compose.yml` environment section.  

### Using a `.env` file
Create a `.env` file in the same folder as `docker-compose.yml`:

```
AZURE_OPENAI_API_KEY=your_azure_key_here
AZURE_OPENAI_ENDPOINT=https://your-azure-endpoint/
AZURE_OPENAI_GPT4_TURBO=your_deployment_name
N8N_BASIC_AUTH_USER=n8n_user
N8N_BASIC_AUTH_PASSWORD=1234
```

### Variables explained
- **DB_TYPE, DB_POSTGRESDB**: Configure n8n to connect to the Postgres database defined in `docker-compose.yml`. Make sure the user/password match the Postgres service.  
- **N8N_BASIC_AUTH**: Enable and set login credentials for the n8n UI. You can provide these in `.env` or directly in the `docker-compose.yml` environment section.  
- **N8N_CORS**: Allow browser-based frontends (like `chatbot.html` on port 3001) to access the n8n API/webhooks during development. This prevents cross-origin errors when your frontend and n8n run on different ports.  

> **Tip:** For local development, you can use either approach—environment variables in `.env` or directly in the Docker environment section. Using `.env` keeps secrets out of version control. Always add `.env` to `.gitignore`.

---

## 🚀 Start the Stack

From the repository root, run:

```sh
docker compose up -d
```

Check running containers from docker desktop application or command line tool:

```sh
docker compose ps
```

Follow logs (helpful while starting):

```sh
docker compose logs -f n8n
```

---

## 🌐 Access the n8n Editor

Open in your browser:

[http://localhost:5678](http://localhost:5678)

Default login (from compose):

- Username: `n8n_user`
- Password: `1234`

**Important:** Change these credentials before using in production.

---

## 🚀 How to Use and Import Workflows

1. Log in to n8n.
2. Click **Workflows → New workflow**.
3. Click the menu (⋯) in top-right → **Import from File**.
4. Import `Asana_Automation/Asana_Automation.json`, `Slack_AI_Agent_Chatbot/Slack AI Agent Chatbot.json`, or `RAG_with_Qdrant_VectorStore/RAG with Qdrant VectorStore.json` files of the workflow you want to use.
5. Configure credentials (e.g., Slack, Asana, Qdrant, Google Drive, etc.)  
6. Save and edit nodes as needed.
7. Activate and run!  

---

## 🔑 Configure Required Credentials

Most workflows need external credentials. In n8n UI:

- Click **Credentials** in the left menu (or open the workflow and click a node that needs a credential).
- Add new credentials for each service used, for example:
  - Asana → Personal Access Token ([guide](https://developers.asana.com/docs/personal-access-token))
  - Slack → OAuth token / Slack App credentials
  - Azure OpenAI / OpenAI / Ollama → API key and endpoint
  - Qdrant → API key / endpoint (for Slack RAG workflow)

---

## 🛑 Stopping & Removing Containers

Stop containers (preserve data):

```sh
docker compose down
```

Stop and delete volumes (delete all stored data):

```sh
docker compose down -v
```

List volumes:

```sh
docker volume ls
```

Remove a named volume:

```sh
docker volume rm <volume_name>
```

---

## 🔒 Security & Production Notes

- Do not use default credentials in production.
- Use strong passwords and secrets manager.
- Do not commit `.env` or secrets to version control.
- Consider HTTPS and a reverse proxy (e.g., nginx) before exposing n8n to the public internet.
- Use separate credentials for production integrations (Asana, Slack, OpenAI, etc.).

---
