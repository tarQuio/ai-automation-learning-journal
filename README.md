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

<p align="center">
  <img src="./screenshots/day-01-workflow.png" alt="Workflow Screenshot" width="100%" />
</p>

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

<p align="center">
  <img src="./screenshots/day-02-workflow.png" alt="Workflow Diagram" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-02-result.png" alt="Telegram Output" width="100%" />
</p>

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

<p align="center">
  <img src="./screenshots/day-03-workflow.png" alt="Workflow Canvas" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-03-sheets.png" alt="Google Sheets Entry" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-03-telegram.png" alt="Telegram Alert" width="100%" />
</p>

---w

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

<p align="center">
  <img src="./screenshots/day-04-workflow.png" alt="Workflow Canvas" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-04-sheets.png" alt="Google Sheets Entry" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-04-telegram.png" alt="Telegram Priority Alert" width="100%" />
</p>

---

## 📅 Day 5: Multi-Modal AI Document & Invoice Processing Pipeline

### 🎯 Objective

Build an automated document and receipt/invoice processing pipeline capable of ingesting binary image uploads via n8n Form Trigger, extracting structured financial data using an AI Agent with Multimodal Vision (Gemini 1.5 Flash), sanitizing dynamic JSON payloads, logging structured transactions into Google Sheets, and dispatching real-time formatted financial reports to Telegram.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Form Trigger, AI Agent Node, Google Sheets Node, Telegram Node)
- **Google Gemini Chat Model** (`gemini-2.5-flash`)
- **Google Sheets API** & **Telegram Bot API**

### 💡 Key Learnings Today

1. Ingested binary image payloads directly from n8n Form Trigger into an AI Agent node connected with Google Gemini Chat Model.
2. Utilized Multimodal Vision capabilities to automatically process image files and extract structured financial fields (`nama_vendor`, `tanggal`, `total_belanja`, `kategori`, `ringkasan_item`).
3. Applied regex string sanitization (`.replace(/```json|```/g, '')`) on `$('AI Agent').item.json.output` to eliminate markdown formatting and prevent `undefined` parsing errors.
4. Built an end-to-end automated financial logging pipeline with real-time Telegram receipt notifications.

### 📷 Workflow & Output

<p align="center">
  <img src="./screenshots/day-05-workflow.png" alt="Workflow Canvas" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-05-sheets.png" alt="Google Sheets Entry" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-05-telegram.png" alt="Telegram Finance Alert" width="100%" />
</p>

---

## 📅 Day 6: RAG-Powered AI Customer Support Bot with Dynamic Knowledge Base & Memory

### 🎯 Objective

Build an intelligent multi-turn Telegram customer support bot powered by an AI Agent. The bot leverages Google Gemini for LLM reasoning, Window Buffer Memory for conversational context retention across messages, and a Google Sheets Tool / Vector Store as a dynamic Knowledge Base (RAG) to process customer queries with precise, grounded responses.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Telegram Trigger, AI Agent Node, Google Sheets Tool, Simple Memory, Telegram Node)
- **Google Gemini Chat Model** (`gemini-2.5-flash`)
- **Google Sheets API** (Knowledge Base / RAG Search)
- **Telegram Bot API** & **ngrok Tunneling**

### 💡 Key Learnings Today

1. **Agentic Workflow**: Understood the architectural differences between a standard LLM Chain and an AI Agent capable of autonomous tool execution and decision-making.
2. **Conversational Memory**: Implemented Window Buffer Memory to maintain multi-turn chat context across ongoing Telegram interactions.
3. **Grounding & RAG (Retrieval-Augmented Generation)**: Prevented AI hallucinations by constraining response generation strictly to verified official FAQ documents stored in the Google Sheets Knowledge Base.
4. **System Prompt & Intent Routing**: Refined system prompt rules to classify user intent—separating conversational greetings from domain-specific inquiries requiring Knowledge Base retrieval.
5. **Infrastructure Recovery**: Restored a corrupted n8n database instance, migrated workflow data and encrypted credentials using `N8N_ENCRYPTION_KEY`, and re-established active webhooks via ngrok.

### 📷 Workflow & Output

<p align="center">
  <img src="./screenshots/day-06-workflow.png" alt="Workflow Canvas" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-06-sheets.png" alt="Google Sheets Knowledge Base" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-06-telegram.png" alt="Telegram Bot Conversation" width="100%" />
</p>
