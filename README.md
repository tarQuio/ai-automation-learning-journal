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

---

## 📅 Day 7: AI Executive Assistant – Multi-Tool Calendar & Task Orchestrator

### 🎯 Objective

Build an autonomous AI Executive Assistant using n8n Agentic Architecture. The workflow accepts natural language instructions via n8n Form, leverages Google Gemini (`gemini-2.5-flash`) as the core reasoning engine with dynamic system prompt time-offset calculations, and dynamically executes multi-tool actions across Google Calendar and Google Tasks before dispatching an execution summary to Telegram.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Form Trigger, AI Agent Node, Google Calendar Tool, Google Tasks Tool, Telegram Node)
- **Google Gemini Chat Model** (`gemini-2.5-flash`)
- **Google Calendar API** & **Google Tasks API**
- **Telegram Bot API**

### 💡 Key Learnings Today

1. **Multi-Tool Agentic Orchestration**: Built an autonomous AI Agent capable of dynamically selecting and executing multiple tools (Google Calendar and Google Tasks) in a single execution pipeline based on natural language intent.
2. **Dynamic Time-Offset Calculations**: Configured Luxon time expressions (`$now.setZone().plus()`) in the system prompt to allow the LLM to calculate relative time references (e.g., "besok", "lusa") accurately in real-time.
3. **Stateless Efficiency**: Optimized workflow architecture by eliminating redundant Memory nodes for stateless single-shot form triggers, reducing execution latency and unnecessary processing overhead.
4. **Tool Argument Alignment**: Configured tool parameters (`summary`, `start`, `end`, `title`) to be dynamically populated by the AI model (`Defined by Model`) using strict ISO 8601 timestamps and clean titles.

### 📷 Workflow & Output

<p align="center">
  <img src="./screenshots/day-07-workflow.png" alt="Workflow Canvas" width="100%" />
</p>

<p align="center">
  <img src="./screenshots/day-07-calendar.png" alt="Google Calendar Output" width="32%" />
  <img src="./screenshots/day-07-tasks.png" alt="Google Tasks Output" width="32%" />
  <img src="./screenshots/day-07-telegram.png" alt="Telegram Notification Output" width="32%" />
</p>

---

## 📅 Day 8: RAG Document Assistant – PDF Ingestion Pipeline with Supabase Vector Store

### 🎯 Objective

Solve a real problem: the official thesis-writing guideline (a 117-page PDF) is hard to search, and students keep flipping through it to find simple formatting rules. This day builds a two-workflow RAG system: one pipeline that ingests the PDF into a vector database, and a Telegram bot that answers questions strictly from the document and cites the page number. Unlike Day 6 (a hand-written FAQ in Google Sheets), the knowledge base here is built automatically from a long document using chunking and embeddings.

### 🛠️ Tech Stack & Nodes Used

- **n8n Self-Hosted** (Form Trigger, Extract From File, Code Node, Loop Over Items, Wait, Supabase Vector Store, Default Data Loader, Recursive Character Text Splitter, Telegram Trigger, AI Agent Node, Telegram Node)
- **Google Gemini** (Embeddings, 3072 dimensions) and Gemini Chat Model for the agent
- **Supabase** (PostgreSQL + `pgvector`) as the vector database
- **Telegram Bot API**

### 🏗️ Architecture

```
Workflow A – Ingestion
Form (upload PDF) → Extract From PDF → Code (split per page, drop empty pages)
  → Loop Over Items (batch size 1) → Supabase Vector Store (Insert)
        ├─ Default Data Loader → Recursive Character Text Splitter (600 / overlap 100)
        └─ Embeddings Google Gemini
  → Wait (2s) → back to loop … → Telegram (done notification)

Workflow B – Q&A
Telegram Trigger → AI Agent ⇄ Supabase Vector Store (retrieve as tool) → Telegram reply with page citation
```

Result: 113 text pages ingested into roughly 360 chunks, each stored with `sumber`, `halaman` (PDF page index) and `halaman_cetak` (printed page number) metadata.

### 💡 Key Learnings Today

1. **Vector store fundamentals**: Chunking (600 characters, 100 overlap), embeddings, and similarity search with `pgvector`, including creating the table and `match_documents` function in Supabase.
2. **Retrieval as an agent tool**: The agent only calls the knowledge base when the tool description and system prompt tell it to, and it must answer strictly from retrieved context and refuse when nothing relevant is found.
3. **Metadata for citations**: Each chunk carries its source page so every answer can cite where it came from, which makes hallucinations easy to spot.
4. **Rate-limit-aware ingestion**: Processing page by page with Loop Over Items (batch size 1), a Wait node, and retry-on-fail instead of embedding hundreds of chunks in one burst.
5. **Embedding consistency**: Documents and queries must use the same embedding model; mixing models produces dimension mismatches (3072 vs 1024) and meaningless similarity scores.

### 🧩 Challenges & Solutions

| Problem                                                                                                      | Cause / Finding                                                                                                                          | Solution                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `vector must have at least 1 dimension` when ingesting the full PDF, while a 5-page PDF worked               | Embedding calls returned empty vectors once the number of chunks grew (5 pages OK, 45 pages failed); suspected request size / rate limit | Split the PDF into one item per page, loop with batch size 1, add a Wait node and retry-on-fail                    |
| Default Data Loader failed with "expects binary file" after switching to page-by-page processing             | The loader was still configured for binary PDF input                                                                                     | Changed Type of Data to JSON and mode to Load Specific Data with the page text expression                          |
| Telegram node flooded the chat with dozens of messages                                                       | The `done` output of the loop carries every processed item (about 360), and Telegram sends one message per item                          | Enabled **Execute Once** on the Telegram node and used a summary message instead of per-item data                  |
| Agent answered without searching the knowledge base                                                          | Weak tool description and permissive system prompt                                                                                       | Rewrote the tool name/description and made the system prompt require tool use for every guideline question         |
| Cited page (43) did not match the printed page (34)                                                          | The PDF index counts the cover and roman-numbered pages, while the document uses printed numbers                                         | Stored both `halaman` and `halaman_cetak` (offset = 9) and made the agent cite the printed page                    |
| Switching to a different embedding model for queries failed with `different vector dimensions 3072 and 1024` | Query embeddings and stored document embeddings came from different models                                                               | Rule adopted: one embedding model for both ingestion and retrieval; switching models means re-ingesting everything |

### ✅ Initial Validation

Asked "what are the margin sizes?" via Telegram. The bot returned 4 cm (top, left) and 3 cm (bottom, right) for Latin script, and cited printed page 34, which matches the original PDF. A full evaluation (15 questions including paraphrased ones, plus 3 out-of-scope questions to test refusal) is documented separately in `docs/day-08-evaluation.md`.

### 🔮 Next Improvement

The Gemini free-tier quota ran out during testing and the bot stopped working. Day 9 will focus on error handling, alerting, and a fallback model so a single quota limit does not take the assistant down.

### 📷 Workflow & Output

![Ingestion Workflow](screenshots/day-08-ingestion-workflow.png)

![Q&A Workflow](screenshots/day-08-qa-workflow.png)

![Supabase Table](screenshots/day-08-supabase.png)

![Telegram Answer with Citation](screenshots/day-08-telegram.png)

---

