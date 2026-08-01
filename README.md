# React Search Agent

A LangChain **ReAct-style search agent** that uses an LLM plus **Tavily** web search to answer questions with structured sources.

## What it does

- Creates an agent with `create_agent` (LangChain)
- Gives the agent a `TavilySearch` tool
- Asks a question (default: AI engineer jobs with LangChain in Berlin)
- Returns a structured `AgentResponse` (`answer`, `content`, `sources`)

## Stack

- Python `>=3.11`
- [uv](https://docs.astral.sh/uv/)
- `langchain-openai`
- `langchain-tavily` / Tavily
- `python-dotenv`

## Setup

```bash
cd react-search-agent
uv sync
```

Create a `.env` in the project root (gitignored):

```env
OPENAI_API_KEY=your_openai_key
TAVILY_API_KEY=your_tavily_key
```

Get a Tavily key at [tavily.com](https://tavily.com).

## Run

```bash
uv run react-search-agent
# or
uv run python -m react_search_agent
```

## Project layout

```text
react-search-agent/
├── src/react_search_agent/
│   └── __init__.py      # agent + main()
├── pyproject.toml
├── uv.lock
├── .env                 # local only
└── README.md
```

## Customize the query

In `src/react_search_agent/__init__.py`, change the `HumanMessage` content inside `main()` to ask a different search question.

## uv commands

Useful commands for this project (run from the project root):

### Environment & install
```bash
uv sync                          # create/update .venv from uv.lock + pyproject.toml
uv sync --upgrade                # upgrade deps within constraints, refresh lock
uv venv                          # create a .venv only (usually uv sync is enough)
uv python pin 3.11               # pin Python version (.python-version)
uv python list                   # list installed/available Python versions
```

### Add / remove packages
```bash
uv add <package>                 # add dependency (updates pyproject.toml + lock)
uv add 'langchain-openai>=1.0'   # add with version constraint
uv add --dev pytest              # add as a development dependency
uv remove <package>              # remove dependency
uv lock                          # refresh uv.lock without installing
uv lock --upgrade                # upgrade all locked versions
```

### Run code
```bash
uv run react-search-agent        # run project script from pyproject.toml
uv run python -m react_search_agent
uv run black .                   # format with Black
uv run isort .                   # sort imports (if isort is added)
uv run python                    # open Python REPL in the project env
```

### Inspect
```bash
uv tree                          # dependency tree
uv pip list                      # packages installed in .venv
uv pip show langchain-openai     # details for one package
uv run which python              # path to env Python
```

### Help
```bash
uv --help
uv add --help
uv run --help
```

Docs: [https://docs.astral.sh/uv/](https://docs.astral.sh/uv/)

## Notes

- Use the project interpreter: `.venv/bin/python`
- Format: `uv run black .`
- Never commit `.env` or API keys
