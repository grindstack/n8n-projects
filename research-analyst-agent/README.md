# 🔍 Research & Analysis Agent

> A **dual-agent AI system** built in n8n that combines real-time web research with deep analytical thinking — you ask a question, it searches the web, thinks it through, and delivers a structured analysis.

---

## 💡 What It Does

You type a question or topic in chat. The **Analysis Agent** receives it, uses a **Think** tool to reason carefully, then delegates live research to the **Research Agent**, which searches the web via **SerpAPI** and returns findings. The Analysis Agent then synthesizes everything into a clear, structured response.

```
You ask a question
    ↓
Analysis Agent (thinks + orchestrates)
    ↓
Research Agent (searches the web)
    ↓
Structured answer back to you
```

---

## 🏗️ Architecture

```
Chat Trigger
    ↓
Analysis Agent
├── Google Gemini (brain)
├── Simple Memory (context)
└── Think (reasoning tool)
        ↓
  Research Agent
  ├── Google Gemini (brain)
  └── SerpAPI (live web search)
```

### The 2 Agents

| Agent | Role |
|---|---|
| **Analysis Agent** | The orchestrator. Receives your input, reasons through it using the Think tool, delegates research, and synthesizes the final answer |
| **Research Agent** | The researcher. Takes a search query from the Analysis Agent, fetches live web results via SerpAPI, and returns raw findings |

---

## 🔧 Tech Stack

| Component | Purpose | Cost |
|---|---|---|
| **n8n** | Workflow automation platform | Free tier |
| **Google Gemini** | AI brain for both agents | Free tier |
| **SerpAPI** | Live Google search results for the Research Agent | Free tier (100 searches/month) |
| **Simple Memory** | Keeps conversation context for the Analysis Agent | Built-in (free) |
| **Think Tool** | Forces the agent to reason step-by-step before acting | Built-in (free) |

---

## 🧠 Node Breakdown

### Analysis Agent
| Node | Type | Role |
|---|---|---|
| **When chat message received** | Trigger | Entry point — catches user input |
| **Analysis Agent** | AI Agent | Main orchestrator |
| **Google Gemini Chat Model 1** | Chat Model | Powers the Analysis Agent's reasoning |
| **Simple Memory** | Memory | Remembers previous messages in the conversation |
| **Think** | Tool | Forces structured step-by-step thinking before responding |

### Research Agent
| Node | Type | Role |
|---|---|---|
| **Research Agent** | AI Agent (sub-agent) | Handles all web search tasks |
| **Google Gemini Chat Model** | Chat Model | Powers the Research Agent |
| **SerpAPI** | Tool | Executes live Google searches and returns results |

---

## 🚀 Example Flow

**Input:** `"What are the latest trends in AI agents for 2026?"`

1. **Chat Trigger** receives the message
2. **Analysis Agent** reads it and calls the **Think** tool to plan its approach
3. **Analysis Agent** delegates to **Research Agent** with a refined search query
4. **Research Agent** calls **SerpAPI** → fetches live Google results
5. **Research Agent** returns structured findings to the Analysis Agent
6. **Analysis Agent** synthesizes everything into a clear, insightful answer
7. Response delivered back to the user in chat

---

## 🧩 Key Concepts

1. **Think Tool = Better Reasoning** — Before acting, the Analysis Agent uses the Think tool to slow down and plan. This reduces hallucination and improves answer quality significantly.

2. **Separation of Concerns** — The Analysis Agent focuses on reasoning and synthesis; the Research Agent focuses only on searching. Each does one thing well.

3. **Live Data via SerpAPI** — Unlike a plain LLM, this system pulls real-time Google search results, making answers current and grounded in actual sources.

4. **Simple Memory for Context** — The Analysis Agent remembers the conversation, so follow-up questions like "tell me more about the second point" work naturally.

5. **Gemini Powers Both Agents** — Using Google Gemini across both agents keeps the stack consistent and fully within the free tier.

---

## ⚠️ Known Gotchas

| Issue | Fix |
|---|---|
| **SerpAPI rate limit** | Free tier allows 100 searches/month. For heavy use, upgrade or use a different search tool |
| **Research Agent not connecting** | The red ✕ on nodes in the screenshot indicates a credentials error — make sure Gemini API key and SerpAPI key are both configured |
| **Vague answers** | Improve the Analysis Agent's system prompt to be more specific about output format (e.g. bullet points, summaries, sources) |
| **No memory on Research Agent** | The Research Agent is stateless by design — it only handles one search task at a time and passes results back |

---

## 🛠️ Skills Used

| Skill | Description |
|---|---|
| **Prompt Engineering** | Writing system prompts that guide each agent to reason and search effectively |
| **Multi-Agent Design** | Structuring an orchestrator + specialist pattern for research workflows |
| **Workflow Automation** | Connecting triggers, agents, memory, and external APIs in n8n |

---

## 🌱 What You Can Build Next

The same pattern works for many research-heavy use cases:

- **Competitor Analysis Tool** — Research Agent searches competitors, Analysis Agent compares and scores them
- **News Summarizer** — Research Agent fetches today's headlines, Analysis Agent summarizes by category
- **Investment Research Assistant** — Research Agent pulls financial news, Analysis Agent identifies key signals
- **Academic Literature Helper** — Research Agent finds papers, Analysis Agent extracts key findings

> *The pattern stays the same. Only the search queries and output format change.*

---

## 📄 License

MIT — free to use, modify, and build upon.

---

*Built with n8n · Google Gemini · SerpAPI · Zero dollars 🚀*
