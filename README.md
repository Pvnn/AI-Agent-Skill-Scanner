# AI Agent Skill Scanner

A FastAPI-based microservice that uses LLMs to perform static code analysis on AI agent skills. The application functions as a cybersecurity auditor, scanning agent skill definitions to identify common vulnerabilities.

## Features

Scans for four critical vulnerability categories:
- **Hardcoded Secrets**: Detects literal, naked API keys, passwords, or webhook URLs.
- **Prompt Injection**: Identifies attempts to override user control or execute unauthorized actions.
- **Excessive Permissions**: Flags network or filesystem permissions that are unjustifiably broad.
- **Unclear Provenance**: Checks for missing metadata or tampered version history.

## Tech Stack

- **FastAPI**: For high-performance API endpoints.
- **OpenAI API (GPT-4o-mini)**: For intelligent vulnerability scanning.
- **Pydantic**: For data validation.

## Setup & Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-dir>
   ```

2. Create a virtual environment and install dependencies:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Configure environment variables:
   Copy the example environment file and add your API key (if using standard OpenAI API, keep the base URL or remove it).
   ```bash
   cp .env.example .env
   ```

4. Run the server:
   ```bash
   uvicorn main:app --reload
   ```

## Usage

Send a POST request to the root endpoint (`/`) with the skill content in JSON format:

```json
{
  "skill": "def custom_skill():\n    api_key = 'sk-123456789'\n    # ... logic ..."
}
```

**Response:**
```json
{
  "categories": ["hardcoded_secret"]
}
```

## Configuration

This project allows you to point to custom OpenAI-compatible endpoints by modifying the `OPENAI_BASE_URL` in your `.env` file. This makes it easily compatible with various AI proxies or self-hosted LLM backends (like Ollama or vLLM).
