# Asana Automation Workflow

This workflow integrates **Asana** with n8n and uses AI to assist project managers in managing tasks.  

---

## 🎯 Purpose
The workflow automates common project management actions in Asana, such as:  
- Fetching tasks from a specific project  
- Summarizing task lists or updates in natural language  
- Adding comments to tasks directly from chat inputs  
- Changing task statuses (e.g., marking tasks as complete)  
- Handling cases where the project or task is not found  

---

## ⚙️ How It Works
1. A **Webhook** receives a user’s query (e.g., from a chat interface).  
2. AI models classify the intent:  
   - *Get tasks*  
   - *Summarize updates*  
   - *Add comment*  
   - *Change status*  
3. The workflow interacts with the **Asana API** to execute the request.  
4. AI generates user-friendly summaries and confirmations.  

---

## 🔑 Requirements
- n8n instance (self-hosted or cloud)  
- Asana API token  
- Azure OpenAI or compatible LLM API (used for intent recognition and summaries)  

---

## 🚀 How to Use
1. Import `Asana_Automation.json` into your n8n instance  
2. Set up credentials:  
   - **Asana**: Provide your personal access token  
   - **OpenAI / Azure OpenAI**: Configure API credentials  
3. Deploy the webhook and integrate it with your preferred interface (Slack, custom app, etc.)  


## 🤖 N8N Asana Workflow Integration with Custom Chatbot

The provided `Asana_Automation/chatbot.html` sends POST requests to:

```
http://localhost:5678/webhook-test/test
```

This matches the Webhook node in the Asana workflow. If you change the webhook path with test/production URL, update `chatbot.html` accordingly.

**Serve the chatbot UI:**

From inside `Asana_Automation/`:

```sh
python -m http.server 3001
```

Then open: [http://localhost:3001/chatbot.html](http://localhost:3001/chatbot.html)

---

## 🔐 Basic Auth & CORS

If Basic Auth is enabled, update `chatbot.html` fetch to include:

```js
const response = await fetch('http://localhost:5678/webhook-test/test', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Basic ' + btoa('n8n_user:1234')
  },
  body: JSON.stringify({ chatInput: message, sessionId: '123456' }),
});
```

---

## 🧪 Test the Chatbot + Workflow

1. Start n8n and import `Asana_Automation.json`.
2. Configure Asana + LLM credentials in n8n.
3. Activate the workflow in n8n.
4. Serve the chatbot and open it in your browser.
5. Test by sending queries like:  
   - Show me tasks in Project Alpha
   - Add a note to Task "Fix login bug": Double-check with QA
   - Mark "Update UI" as complete
---

## 📌 Example Use Case
👉 A project manager types into chat:  
“Add a note to the *UI Fixes* task that says ‘Recheck after QA testing’.”  

✔️ The workflow extracts the task and comment → adds it in Asana → confirms back in chat.  

---
