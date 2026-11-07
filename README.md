# Flag Finding Agentic Loop

A CTF-style challenge where an LLM-powered agent is placed in a "time loop" to find a hidden codeword embedded within its own source code.

## Overview

The project consists of a Python script (`main.py`) that orchestrates an agentic loop using [Ollama](https://ollama.com/). The agent is given a system prompt that challenges it to:
1. Explore the system filesystem.
2. Locate the source code of the script currently executing.
3. Extract a hidden codeword (`SECRET`).

## How it Works

1. **The Loop**: The script maintains a conversation history with the LLM.
2. **Structured Output**: The agent must respond in JSON format, providing:
   - `command`: A PowerShell command to execute.
   - `timeout_seconds`: How long to wait for the command.
   - `comments`: Reasoning for the action.
   - `hidden_code`: The discovered codeword (if found).
3. **Execution**: The script runs the provided PowerShell commands from the system root (`C:\`) and feeds the output back into the LLM's history.
4. **Termination**: The loop ends when the agent successfully provides the correct codeword.

## Technical Details

- **Language**: Python 3
- **LLM**: Configured for `gemma4` via Ollama.
- **Shell**: PowerShell (pwsh or powershell.exe).
- **Dependencies**: `ollama`, `pydantic`.

## Getting Started

### Prerequisites
- Install [Ollama](https://ollama.com/).
- Pull the required model: `ollama pull gemma4`.
- Install Python dependencies:
  ```bash
  pip install ollama pydantic
  ```

### Running the Challenge
```bash
python main.py
```

## Files
- `main.py`: The core engine of the agentic loop.
- `logs.txt`: Automatically generated log of the conversation history.
