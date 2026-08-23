# 🦜️🔗 LangChain Update (v1.x & LangGraph)

A hands-on, modern repository exploring the latest **LangChain v1.x** architecture, **LangGraph** agent orchestration, and multi-provider LLM integrations with **Google Gemini**, **OpenAI**, and **Groq**.

---

## 🚀 Key Highlights

- **Modern LangChain (v1.x)**: Uses the updated LangChain APIs, including `create_agent` with built-in StateGraph execution.
- **LangGraph Integration**: Agent execution runs on `CompiledStateGraph` under the hood for robust state management and multi-turn workflows.
- **Multi-Provider LLM Support**:
  - 🤖 **Google GenAI / Gemini** (`langchain-google-genai`): Gemini 2.5 Flash, Gemini 3.7 Flash
  - 🧠 **OpenAI** (`langchain-openai`): GPT-4o, GPT-4o-mini
  - ⚡ **Groq** (`langchain-groq`): Llama 3, Mixtral high-speed inference
- **Fast Package Management with `uv`**: Uses Astrals's `uv` for lightning-fast, reproducible dependency management (`pyproject.toml` + `uv.lock`).

---

## 📁 Project Structure

```text
langchainupdate/
├── .env.example              # Template for API keys
├── .gitignore                # Git ignore rules (protects API keys & checkpoints)
├── pyproject.toml            # Project metadata and dependencies
├── requirements.txt          # Exported dependency list
├── uv.lock                   # Dependency lockfile
├── src/
│   └── langchainupdate/
│       └── __init__.py       # Package entrypoint
└── updatedlangchain/
    ├── 1-langchainintro.ipynb     # Modern LangChain v1 intro, tools, & agents
    └── 2-modelintegration.ipynb   # Multi-provider model integrations
```

---

## 🛠️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/ashishkamble738/langchainupdate.git
cd langchainupdate
```

### 2. Set Up Environment

Using **`uv`** (Recommended):

```bash
# Create virtual environment and install all dependencies
uv sync

# Or add dependencies from requirements.txt
uv add -r requirements.txt
```

Using standard **`pip`**:

```bash
python -m venv .venv
# On Windows:
.venv\Scripts\activate
# On Linux/macOS:
source .venv/bin/activate

pip install -r requirements.txt
```

---

## 🔑 Environment Variables Configuration

Copy `.env.example` to `.env` and fill in your API keys:

```bash
cp .env.example .env
```

Edit `.env`:

```env
OPENAI_API_KEY="your-openai-api-key"
GROQ_API_KEY="your-groq-api-key"
GOOGLE_API_KEY="your-google-api-key"
```

---

## 📖 Notebooks Overview

| Notebook | Description |
| :--- | :--- |
| **[`1-langchainintro.ipynb`](updatedlangchain/1-langchainintro.ipynb)** | Getting started with LangChain v1, defining custom tools with Python type hints, creating agents via `create_agent`, and invoking them with tool calling. |
| **[`2-modelintegration.ipynb`](updatedlangchain/2-modelintegration.ipynb)** | Integrating and comparing multiple LLM providers (Google Gemini, OpenAI, Groq) within LangChain workflows. |

---

## 💡 Quick Code Example: Building an Agent

Here is how modern agents are constructed using `create_agent` in LangChain v1:

```python
import os
from dotenv import load_dotenv
from langchain.agents import create_agent

load_dotenv()

# Define a tool
def get_weather(city: str) -> str:
    """Get the current weather for a city."""
    return f"The weather in {city} is sunny."

# Create an agent using Google Gemini
agent = create_agent(
    model="google_genai:gemini-3.7-flash",  # or "openai:gpt-4o-mini", "groq:llama-3.3-70b-versatile"
    tools=[get_weather],
    system_prompt="You are a helpful assistant."
)

# Run the agent
response = agent.invoke({
    "messages": [{"role": "user", "content": "What is the weather like in New York?"}]
})

print(response["messages"][-1].content)
```

---

## 📦 Dependencies

- **`langchain`** (>= 1.3.16)
- **`langgraph`** (>= 1.2.11)
- **`langchain-google-genai`** (>= 4.3.5)
- **`langchain-openai`** (>= 1.6.0)
- **`langchain-groq`** (>= 1.1.3)
- **`langchain-community`** (>= 0.4.2)
- **`python-dotenv`** (>= 1.2.3)
- **`ipykernel`** (>= 7.3.0)

---

## 👤 Author

- **Ashish Kamble** ([@ashishkamble738](https://github.com/ashishkamble738))
