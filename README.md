
# 📄 DocDacity – Intelligent Document Assistant

DocDacity is a multi-agent AI assistant built with **LangChain** and **LangGraph** that can analyze, summarize, and perform calculations on structured documents such as invoices, contracts, and claims.

---

## 🚀 Features

- **🔍 Question Answering (Q&A)**  
  Ask questions about documents and get precise answers with source references.

- **📝 Summarization**  
  Generate structured summaries of documents (financial or healthcare).

- **🧮 Calculation Engine**  
  Perform computations on document data using a tool-based approach (all calculations are tool-executed).

- **🧠 Multi-Agent Architecture**  
  Intelligent routing between specialized agents:
  - Q&A Agent  
  - Summarization Agent  
  - Calculation Agent  

- **💾 Persistent Memory**  
  Maintains conversation context across interactions using LangGraph state and checkpointer.

---

## 🏗️ Architecture

The assistant is powered by a **LangGraph workflow**:

```

classify_intent
↓
[qa_agent | summarization_agent | calculation_agent]
↓
update_memory
↓
END

```

Workflow steps:
1. Classify user intent  
2. Route to the appropriate agent  
3. Execute retrieval / reasoning / tools  
4. Update memory and conversation state  

---

## 📁 Project Structure

```

doc_assistant_project/
├── src/
│   ├── schemas.py        # Pydantic models
│   ├── retrieval.py      # Document retrieval logic
│   ├── tools.py          # Calculator, search, reader tools
│   ├── prompts.py        # Prompt templates
│   ├── agent.py          # LangGraph workflow
│   └── assistant.py      # Main assistant runtime
├── sessions/             # Conversation sessions
├── logs/                 # Tool usage logs
├── docs/                 # Architecture diagrams
├── main.py               # Entry point
├── pyproject.toml        # Project config (uv)
└── README.md

````

---

## ⚙️ Requirements

- Python **3.9+**
- OpenAI API key
- [`uv`](https://github.com/astral-sh/uv) package manager

---

## 📦 Installation (using `uv`)

### 1. Install uv

```bash
pip install uv
````

---

### 2. Clone the repository

```bash
git clone https://github.com/eljandoubi/doc_assistant_project.git
cd doc_assistant_project
```

---

### 3. Install dependencies

```bash
uv sync
```

This will automatically:

* Create a virtual environment
* Install all dependencies from `pyproject.toml`

---

## 🔑 Environment Setup

Create your environment file:

```bash
cp .env.example .env
```

Then add your API key:

```env
OPENAI_API_KEY=your_api_key_here
```

---

## ▶️ Running the Assistant

Start the application with:

```bash
uv run main.py
```

---

## 💬 Example Queries

You can interact with the assistant using natural language:

* "What's the total amount in invoice INV-001?"
* "Summarize all contracts"
* "Calculate the sum of all invoice totals"
* "Find documents with amounts over $50,000"
* "Show invoices under $10,000"

---

## 🧰 Tools System

The assistant uses four core tools:

### 🔍 Document Search Tool

Finds relevant documents using keyword, type, or amount filters.

### 📄 Document Reader Tool

Retrieves full content of a specific document by ID.

### 🧮 Calculator Tool

Performs **all mathematical operations** safely using validated expressions.

### 📊 Statistics Tool

Provides aggregate insights across the document collection.

All tool usage is:

* Logged automatically
* Tracked per session
* Stored in `./logs/`

---

## 🧠 Key Design Principles

### 1. Multi-Agent Routing

User input is classified into:

* `qa`
* `summarization`
* `calculation`

Then routed to the correct specialized agent.

---

### 2. Structured Outputs

All LLM responses use **Pydantic schemas** to ensure:

* Type safety
* Consistent formatting
* Reliable parsing

---

### 3. Tool-Based Reasoning

The LLM does NOT compute directly.

Instead it:

1. Extracts data
2. Builds expressions
3. Uses the calculator tool
4. Returns validated results

---

### 4. Persistent Memory

LangGraph checkpointer enables:

* Conversation continuity
* Document tracking
* State persistence across turns

---

## 🧪 Development

Run the project in development mode:

```bash
uv run python main.py
```

Logs are stored in:

```
./logs/
```

Sessions are stored in:

```
./sessions/
```

---


## 📌 Future Improvements

* Replace `eval()` with a safe math parser (`ast` or `sympy`)
* Improve document retrieval ranking using embeddings
* Add web UI (Streamlit or React frontend)
* Add streaming responses for agents
* Improve error recovery in workflow nodes

---

