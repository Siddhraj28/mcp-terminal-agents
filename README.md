# mcp-terminal-agents

An MCP (Model Context Protocol) server that gives an AI agent terminal-like capabilities — running shell commands, executing Python, and reading/writing files — through a simple set of tools.

Built with [FastMCP](https://github.com/jlowin/fastmcp).

📦 Published on PyPI: **[mcp_terminal_agents](https://pypi.org/project/mcp_terminal_agents/)**

## Features

This server exposes the following tools to any MCP-compatible client:

| Tool | Description |
|---|---|
| `bash(command)` | Executes a shell command and returns its output |
| `python_code(code)` | Executes a Python code string and returns its output |
| `python_file(file)` | Executes a Python file and returns its output |
| `glob(pattern)` | Returns a list of files matching a glob pattern |
| `grep(pattern, file)` | Searches for a pattern within a file |
| `read_file(file)` | Reads and returns the contents of a file |
| `write_file(file, content)` | Writes content to a file (creates it if missing) |
| `create_folder(folder)` | Creates a new folder |
| `delete_folder(folder)` | Deletes a folder and its contents |

## Installation

Install from PyPI:

```bash
pip install mcp_terminal_agents
```

Or, for local development, using [uv](https://docs.astral.sh/uv/):

```bash
git clone https://github.com/Siddhraj28/mcp-terminal-agents.git
cd mcp-terminal-agents
uv sync
```

## Usage

Run the server directly:

```bash
mcp_terminal_agents
```

This starts the MCP server over `stdio` transport, ready to be connected to an MCP client (e.g. Claude Desktop, Claude Code, or any other MCP-compatible agent).

### Example MCP client config

```json
{
  "mcpServers": {
    "terminal-agents": {
      "command": "mcp_terminal_agents"
    }
  }
}
```

## Requirements

- Python >= 3.13
- [fastmcp](https://pypi.org/project/fastmcp/) >= 4.0.5

## Security Note

This server executes arbitrary shell commands and Python code on the host machine with no sandboxing. Only connect it to trusted agents/clients, and avoid exposing it to untrusted input or network-facing environments.

## Project Structure

```
mcp-pypi/
├── src/
│   └── mcp_terminal/
│       ├── main.py       # Entry point, starts the MCP server
│       └── tools.py      # Tool definitions (bash, file ops, etc.)
├── main.py                # Simple standalone script
├── pyproject.toml
└── uv.lock
```


