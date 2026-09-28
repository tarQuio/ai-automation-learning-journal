# 🚀 n8n & AI Automation Learning Journal

Daily documentation on building workflow automations with n8n and AI.

---

## 📅 Day 1: Email-to-Telegram Notification Workflow

### 🎯 Objective

Automate tracking of incoming emails by extracting essential metadata (Sender, Subject, Snippet) and delivering instant structured alerts directly to a Telegram channel.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Gmail Trigger, Code Node, Telegram Node)
- **Google Workspace API** (OAuth2)
- **Telegram Bot API**

### 💡 Key Learnings Today

1. Connected Gmail trigger using OAuth2 authentication in n8n self-hosted.
2. Extracted and formatted nested JSON properties (`from`, `subject`, `snippet`) via JavaScript Code Node.
3. Configured custom Telegram Bot messaging with Markdown formatting.

### 📷 Workflow Visual & Output

![Workflow Screenshot](./screenshots/day-01-workflow.png)

---

## 📅 Day 2: AI Email Summarizer & Urgency Classifier

### 🎯 Objective

Streamline email processing by connecting a Gmail trigger directly to an LLM via Basic LLM Chain to generate concise 2-sentence summaries and analyze urgency levels before sending alerts to Telegram.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Gmail Trigger, Basic LLM Chain, Telegram Node)
- **Groq Chat Model** (LLM Integration)
- **Telegram Bot API**

### 💡 Key Learnings Today

1. Implemented a streamlined 3-node architecture for efficient single-prompt AI processing.
2. Formatted prompt templates to output structured text without over-engineering with complex Agent nodes.
3. Successfully dynamically mapped AI outputs and email metadata into Telegram notification templates.

### 📷 Workflow & Result

![Workflow Diagram](./screenshots/day-02-workflow.png)
![Telegram Output](./screenshots/day-02-result.png)
