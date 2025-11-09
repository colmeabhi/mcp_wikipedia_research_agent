# Wikipedia MCP Research Agent

A Model Context Protocol (MCP) server and client implementation that enables AI agents to search and retrieve information from Wikipedia using Google's Gemini AI.

## Features

- 🔍 Wikipedia search and article retrieval via MCP server
- 🤖 AI-powered research agent using Google Gemini 2.5 Flash
- 🛠️ MCP tools integration with LangGraph
- 💬 Interactive command-line interface
- 📚 Support for prompts and resources via MCP protocol

## Prerequisites

- Python 3.13 or higher
- Google AI API key (Gemini API)
- Git

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/mcp_wikipedia_research_agent.git
cd mcp_wikipedia_research_agent
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

If `requirements.txt` doesn't exist, install the required packages:

```bash
pip install mcp wikipedia langchain-google-genai langchain-mcp-adapters langgraph python-dotenv
```

### 4. Set Up Environment Variables

1. Copy the example environment file:
```bash
cp .env.example .env
```

2. Get your Google AI API key:
   - Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
   - Click "Create API key"
   - Copy your API key

3. Edit `.env` and add your API key:
```bash
# Open .env in your editor
nano .env

# Add your API key (replace with your actual key):
GOOGLE_API_KEY=your-actual-api-key-here
```

**⚠️ IMPORTANT: Never commit your `.env` file to GitHub!** It's already listed in `.gitignore`.

## Usage

### Running the Wikipedia MCP Agent

Start the interactive agent:

```bash
python mcp_client.py
```

### Available Commands

Once the agent is running, you can use the following commands:

- **Ask questions naturally**: Just type your question
  ```
  You: Tell me about Python programming
  ```

- **List available prompts**:
  ```
  You: /prompts
  ```

- **Run a specific prompt**:
  ```
  You: /prompt <prompt_name> "argument1" "argument2"
  ```

- **List available resources**:
  ```
  You: /resources
  ```

- **View a specific resource**:
  ```
  You: /resource <resource_name>
  ```

- **Exit the agent**:
  ```
  You: exit
  ```
  Or use `quit` or `q`

### Example Session

```
Wikipedia MCP agent is ready.
Type a question or use the following templates:
  /prompts                - to list available prompts
  /prompt <name> "args"   - to run a specific prompt
  /resources              - to list available resources
  /resource <name>        - to run a specific resource

You: What is machine learning?
AI: [Agent searches Wikipedia and provides information about machine learning]

You: exit
```

## Project Structure

```
mcp_wikipedia_research_agent/
├── mcp_server.py           # MCP server implementation with Wikipedia tools
├── mcp_client.py           # Interactive client with Gemini AI agent
├── .env.example            # Example environment variables (safe to commit)
├── .env                    # Your actual API keys (DO NOT commit)
├── .gitignore              # Git ignore rules (protects credentials)
├── README.md               # This file
└── requirements.txt        # Python dependencies (if created)
```

## How It Works

1. **MCP Server** (`mcp_server.py`):
   - Provides Wikipedia search and retrieval tools
   - Implements the Model Context Protocol
   - Exposes tools, prompts, and resources

2. **MCP Client** (`mcp_client.py`):
   - Connects to the MCP server
   - Uses Google Gemini 2.5 Flash for AI responses
   - Integrates MCP tools with LangGraph
   - Provides interactive command-line interface

3. **Flow**:
   ```
   User Question → Gemini AI → MCP Tools → Wikipedia → AI Response
   ```

## Supported Models

The client uses **Gemini 2.5 Flash** by default. Other supported models include:

- `gemini-2.5-flash` (default - best price/performance)
- `gemini-2.5-flash-lite` (fastest and most cost-efficient)
- `gemini-2.5-pro` (advanced reasoning for complex tasks)

To change the model, edit `mcp_client.py`:

```python
llm = ChatGoogleGenerativeAI(model="gemini-2.5-pro", temperature=0, google_api_key=api_key)
```

## Troubleshooting

### "GOOGLE_API_KEY environment variable is not set"

Make sure you:
1. Created the `.env` file from `.env.example`
2. Added your actual API key to `.env`
3. The `.env` file is in the same directory as `mcp_client.py`

### "API key expired" or "API_KEY_INVALID"

Your API key may be invalid or expired:
1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Create a new API key
3. Update your `.env` file with the new key

### "models/gemini-x.x-xxx is not found"

You may be using a deprecated model name. Update to current models:
- Use `gemini-2.5-flash` instead of `gemini-1.5-flash`
- See the "Supported Models" section above

### Import Errors

Make sure all dependencies are installed:
```bash
pip install -r requirements.txt
```

Or install manually:
```bash
pip install mcp wikipedia langchain-google-genai langchain-mcp-adapters langgraph python-dotenv
```

## Security Notes

🔒 **Protecting Your Credentials:**

1. **Never commit `.env` files** - They contain your API keys
2. The `.gitignore` file prevents `.env` from being committed
3. Only commit `.env.example` with placeholder values
4. If you accidentally commit credentials:
   - Revoke the API key immediately
   - Create a new one
   - Use `git filter-branch` or BFG Repo-Cleaner to remove it from history

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

**Remember:** Never commit your `.env` file!

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)
- [LangChain](https://python.langchain.com/)
- [Google Gemini API](https://ai.google.dev/gemini-api)
- [Wikipedia API](https://www.mediawiki.org/wiki/API:Main_page)

## Support

For issues, questions, or contributions, please open an issue on GitHub.
