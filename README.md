# MCP-powered Agentic RAG using Bright Data and Qdrant

This project implements a Retrieval-Augmented Generation (RAG) system powered by MCP (Model Context Protocol) that combines local knowledge base search with web search capabilities. It uses AI agents to:
- Retrieve information from a local ML knowledge base
- Fall back to web search using [Bright Data](https://brdta.com/dailydoseofds) when needed
- Store and search vectors efficiently using Qdrant as the local vector database
- All integrated seamlessly with Cursor IDE as the MCP client

## Features
- **ML FAQ Search**: Retrieve answers from a curated ML knowledge base using semantic search
- **Web Search Fallback**: Automatically search the web via Bright Data when local knowledge is insufficient
- **Vector Search**: Efficient semantic search using Qdrant vector database
- **MCP Integration**: Seamless integration with Cursor IDE through MCP tools

---
## Setup and installations

**Get BrightData API Key**:
- Go to [Bright Data](https://brdta.com/dailydoseofds) and sign up for an account.
- Select "Proxies & Scraping" and create a new "SERP API"
- Select "Native proxy-based access"
- You will find your username and password there.
- Store it in the .env file.

```
BRIGHDATA_USERNAME="..."
BRIGHDATA_PASSWORD="..."
```

**Install Dependencies**:
   Ensure you have Python 3.11 or later installed.
   ```bash
   pip install mcp qdrant-client
   ```

---

## Run the project

First, start a Qdrant docker container as follows (make sure you have downloaded Docker):

   ```bash
   docker run -p 6333:6333 -p 6334:6334 \
   -v $(pwd)/qdrant_storage:/qdrant/storage:z \
   qdrant/qdrant
   ```

Next, go to the notebook.ipynb file, run the code to create a collection in your vector database.

Finally, set up your local MCP server as follows:
- Go to Cursor settings
- Select MCP 
- Add new global MCP server.

In the JSON file, add this:
```json
{
  "mcpServers": {
      "mcp-rag-app": {
          "command": "python",
          "args": ["/absolute/path/to/server.py"],
          "host": "127.0.0.1",
          "port": 8080,
          "timeout": 30000
      }
  }
}
```

Done! You can now interact with your vector database and fallback to web search if needed.

---

## Contribution

Contributions are welcome! Please fork the repository and submit a pull request with your improvements.
