# MCP LLMS-TXT Server Setup Guide

## Prerequisites
- Python 3.10 or higher
- `uv` package manager

## Installation Steps

1. **Install UV Package Manager**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

2. **Create and Activate Virtual Environment**
```bash
# Create virtual environment using uv
uv venv

# Activate the virtual environment
source .venv/bin/activate
```

3. **Install Project Dependencies**
```bash
# Install the project in editable mode with all dependencies
uv pip install -e .
```

4. **Verify Installation**
```bash
mcpdoc --version
```
Should show the current version (e.g., `mcpdoc 0.0.7`)

## Running the Server

### Basic Usage
```bash
mcpdoc --urls LangGraph:https://langchain-ai.github.io/langgraph/llms.txt \
    --transport sse \
    --port 8082 \
    --host localhost
```

### With All Domains Allowed (Development Mode)
```bash
mcpdoc --urls LangGraph:https://langchain-ai.github.io/langgraph/llms.txt \
    --allowed-domains '*' \
    --transport sse \
    --port 8082 \
    --host localhost
```

### Using Configuration File
```bash
mcpdoc --yaml sample_config.yaml \
    --transport sse \
    --port 8082 \
    --host localhost
```

## Important Parameters
- `--transport sse`: Enables web interface
- `--port 8082`: Sets the server port
- `--host localhost`: Sets the host address
- `--allowed-domains`: Specifies allowed domains for fetching documentation
  - Use `'*'` to allow all domains
  - Or specify specific domains: `domain1.com domain2.com`

## Testing the Server
1. Once running, access the server at: http://localhost:8082
2. Install and run MCP inspector (optional):
```bash
npx @modelcontextprotocol/inspector
```

## Troubleshooting
- If you get domain access errors, make sure to use the `--allowed-domains` parameter
- Ensure you're in the activated virtual environment (should see `(mcpdoc)` in terminal)
- Use `uv pip` instead of `pip` for any package installations

## Note on Security
By default, the server only allows fetching documentation from domains hosting the specified `llms.txt` files. Use `--allowed-domains` to explicitly allow additional domains.
