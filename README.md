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

---

## 📅 Day 3: Webhook Lead Ingestion, AI Sentiment/Action Processing & Database Logging

### 🎯 Objective

Build a real-time data ingestion pipeline using Webhooks to parse inbound lead payloads, process text with LLM for sentiment classification and actionable next steps, dynamically log structured records into Google Sheets, and dispatch notifications via Telegram.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Webhook Trigger, Basic LLM Chain, Google Sheets Node, Telegram Node)
- **Groq Chat Model** (LLM Integration)
- **Google Sheets API** (OAuth2 / Service Account)
- **Telegram Bot API**
- **cURL / Postman** (Testing Trigger)

### 💡 Key Learnings Today

1. Configured Webhook Triggers to handle incoming JSON POST payloads.
2. Formatted prompt instructions to return pure JSON output containing multi-field metadata (`sentimen` & `tindakan`).
3. Parsed stringified JSON responses using expression mode `JSON.parse()` for seamless mapping into database rows and chat alert templates.
4. Integrated automated row appending to maintain a structured lead database on Google Sheets.

### 📷 Workflow & Output

![Workflow Canvas](./screenshots/day-03-workflow.png)
![Google Sheets Entry](./screenshots/day-03-sheets.png)
![Telegram Alert](./screenshots/day-03-telegram.png)

---

## 📅 Day 4: AI-Powered Smart Lead Router & Conditional Escalation

### 🎯 Objective

Build an automated lead triage and escalation pipeline that classifies incoming message payloads by urgency and category using LLM, then dynamically routes them using conditional logic nodes (Switch) to trigger instant Telegram escalation for URGENT tickets or standard background logging for routine requests.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Webhook Trigger, Basic LLM Chain, Switch Node, Google Sheets Node, Telegram Node)
- **Groq Chat Model** (LLM Classifier)
- **Google Sheets API** & **Telegram Bot API**
- **cURL / Postman**

### 💡 Key Learnings Today

1. Designed multi-branch routing workflows using n8n Switch nodes based on AI evaluation results.
2. Formatted prompt templates for zero-shot classification returning JSON structure (`urgensi`, `kategori`, `ringkasan`).
3. Mapped upstream node data explicitly across long-chain branches (`$('Basic LLM Chain').item.json.text`) to avoid undefined payload bugs.
4. Implemented priority-based alerting to prevent notification fatigue while securing critical escalation events.

### 📷 Workflow & Output

![Workflow Canvas](./screenshots/day-04-workflow.png)
![Google Sheets Entry](./screenshots/day-04-sheets.png)
![Telegram Priority Alert](./screenshots/day-04-telegram.png)
