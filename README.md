# 🤖 Multi-Agent Research System

An AI-powered **Multi-Agent Research System** built with **LangChain, LangGraph, Groq, Tavily, BeautifulSoup, and Streamlit**.

The system automatically searches the web, extracts detailed information from relevant webpages, generates a structured research report, and reviews the generated report using an AI critic.

---

## 🚀 Features

* 🔎 **Web Search Agent** – Searches the web for recent and relevant information using Tavily.
* 🌐 **Web Scraping Agent** – Selects relevant resources and extracts webpage content.
* ✍️ **Research Writer** – Generates a structured and professional research report.
* 🧐 **Research Critic** – Reviews the generated report and identifies strengths and areas for improvement.
* 🤖 **LLM-powered agents** – Uses Groq-hosted LLMs through LangChain.
* 🔗 **Tool Calling** – Agents can interact with external tools such as web search and webpage scraping.
* 📊 **Streamlit UI** – Provides an interactive interface for running research tasks.
* 🧩 **Modular architecture** – Search, scraping, writing, and criticism are separated into independent components.
* 🛡️ **Environment variables** – API keys are stored securely using `.env`.

---

## 🏗️ System Architecture

```text
                   User
                     │
                     ▼
              Streamlit Interface
                     │
                     ▼
             ┌─────────────────┐
             │  Search Agent   │
             └────────┬────────┘
                      │
                      ▼
                Tavily Search
                      │
                      ▼
             ┌─────────────────┐
             │  Reader Agent   │
             └────────┬────────┘
                      │
                      ▼
              Web Scraping Tool
                      │
                      ▼
             ┌─────────────────┐
             │ Research Writer │
             └────────┬────────┘
                      │
                      ▼
             ┌─────────────────┐
             │  Research       │
             │    Critic       │
             └────────┬────────┘
                      │
                      ▼
              Final Research Report
```

---

## 🧠 How the System Works

### 1. Search Agent

The Search Agent receives the user's research topic and searches the web using Tavily.

Example:

```text
User:
"What is the impact of artificial intelligence on healthcare?"
```

The Search Agent searches for:

* Recent information
* Reliable sources
* Relevant articles
* Supporting evidence

---

### 2. Reader Agent

The Reader Agent receives the search results and identifies relevant URLs.

It then uses the `scrape_url` tool to retrieve webpage content.

The scraper uses:

* `Requests`
* `BeautifulSoup`
* `lxml`

The parser can handle both HTML and XML responses.

---

### 3. Research Writer

The Writer receives:

```text
Search Results
+
Scraped Content
```

and generates a structured report containing:

```text
Introduction

Key Findings
    ├── Finding 1
    ├── Finding 2
    └── Finding 3

Conclusion

Sources
```

---

### 4. Research Critic

The generated report is passed to a separate AI critic.

The critic evaluates:

```text
Score: X/10

Strengths:
- ...
- ...

Areas to Improve:
- ...
- ...

One line verdict:
...
```

This creates an additional quality-control stage in the research pipeline.

---

# 🛠️ Technologies Used

| Technology    | Purpose                           |
| ------------- | --------------------------------- |
| Python        | Core programming language         |
| LangChain     | LLM and agent framework           |
| LangGraph     | Agent execution and orchestration |
| Groq          | LLM inference                     |
| Tavily        | Web search                        |
| BeautifulSoup | Webpage parsing                   |
| lxml          | XML/HTML parsing                  |
| Requests      | HTTP requests                     |
| Streamlit     | Web interface                     |
| python-dotenv | Environment variable management   |

---

# 📁 Project Structure

```text
MultiAgentSystem/
│
├── app.py
├── agents.py
├── tools.py
├── pipeline.py
├── requirements.txt
├── .env
├── .gitignore
└── README.md
```

### `app.py`

Contains the Streamlit user interface and connects the UI to the research pipeline.

### `agents.py`

Contains:

* Search Agent
* Reader Agent
* Writer Chain
* Critic Chain
* LLM configuration

### `tools.py`

Contains external tools used by the agents:

```python
web_search()
scrape_url()
```

### `pipeline.py`

Coordinates the complete research workflow.

### `requirements.txt`

Contains all Python dependencies required to run the project.

---

# ⚙️ Installation

## 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/MultiAgentSystem.git
```

Move into the project directory:

```bash
cd MultiAgentSystem
```

---

## 2. Create a virtual environment

### Windows

```powershell
python -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\activate
```

---

## 3. Install dependencies

Using `uv`:

```powershell
uv pip install -r requirements.txt
```

Or using pip:

```powershell
pip install -r requirements.txt
```

---

# 🔑 API Keys

Create a `.env` file in the project root.

```env
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

### Groq API

Create your API key from the Groq developer console.

### Tavily API

Create a Tavily API key for web search.

⚠️ **Never upload your `.env` file to GitHub.**

Add this to `.gitignore`:

```gitignore
.env
.venv/
__pycache__/
*.pyc
```

---

# ▶️ Running the Project

## Run the command-line pipeline

```powershell
python pipeline.py
```

You will be asked:

```text
Enter a research topic:
```

Enter a topic such as:

```text
Impact of Artificial Intelligence on Healthcare
```

---

## Run Streamlit

```powershell
streamlit run app.py
```

The application will start locally.

Open:

```text
http://localhost:8501
```

---

# 🔄 Research Workflow

```text
User enters topic
        │
        ▼
Search Agent
        │
        ▼
Tavily Web Search
        │
        ▼
Search Results
        │
        ▼
Reader Agent
        │
        ▼
Relevant URLs
        │
        ▼
BeautifulSoup + Requests
        │
        ▼
Scraped Content
        │
        ▼
Research Writer
        │
        ▼
Generated Report
        │
        ▼
Research Critic
        │
        ▼
Final Reviewed Report
```

---

# 🧪 Example

### Input

```text
Impact of Generative AI on Software Development
```

### Processing

```text
Search
  ↓
Collect sources
  ↓
Scrape relevant sources
  ↓
Combine research
  ↓
Generate report
  ↓
Critique report
```

### Output

The system generates a report containing:

* Introduction
* Key findings
* Conclusion
* Sources
* Critic feedback

---

# 🔐 Security

API keys are loaded using environment variables:

```python
from dotenv import load_dotenv

load_dotenv()
```

Keys should **never** be hardcoded:

```python
# ❌ Don't do this

GROQ_API_KEY = "gsk_xxxxxxxxx"
```

Instead:

```python
# ✅ Correct

import os

api_key = os.getenv("GROQ_API_KEY")
```

---

# 📌 Important Notes

The quality of the final report depends on:

* Search results returned by Tavily
* Availability and accessibility of webpages
* Quality of scraped content
* LLM response quality
* API rate limits
* Website restrictions such as robots rules or dynamic pages

Some webpages may not be accessible through standard HTTP scraping.

---

# 🔮 Future Improvements

Possible future enhancements include:

* 📚 PDF/document research
* 🗄️ Vector database integration
* 🧠 Long-term research memory
* 🔍 Multi-source fact verification
* 📑 Automatic PDF report generation
* 📊 Research analytics dashboard
* 🔄 Parallel research agents
* 🌐 Support for multiple search providers
* 📝 Citation management
* 💬 Conversational research assistant
* ⚡ Parallel agent execution with LangGraph
* 🧪 Automated report quality evaluation

---

# 🎯 Learning Objectives

This project demonstrates practical implementation of:

* Large Language Models
* AI Agents
* Tool Calling
* LangChain
* LangGraph
* Web Search
* Web Scraping
* Prompt Engineering
* LLM Pipelines
* Multi-Agent Architecture
* Streamlit Application Development
* API Integration
* Environment Variable Management

---

# 👨‍💻 Author

**Anuj Sharma**

MCA | AI / Machine Learning | Java Backend Development

---

## ⭐ If you found this project useful

Feel free to ⭐ star the repository and explore the implementation.
