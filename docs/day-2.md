# Day 2: Hello Agents

## [Build agents with Agent Config](https://www.kaggle.com/whitepaper-introduction-to-agents)

### Create the Config Agent
```sh
uv add google-adk
source .venv/bin/activate
cd agents
adk create --type=config basic_agent --model=gemini-2.5-flash
1. Google AI
2. Vertex AI
Choose a backend (1, 2): 1

Don't have API Key? Create one in AI Studio: https://aistudio.google.com/apikey

Enter Google API key: ****************************

Agent created in ./agents/basic_agent:
- .env
- __init__.py
- root_agent.yaml
```

### Run the Config Agent

Explore agent config

```yaml
name: root_agent
model: gemini-2.5-flash
description: A helpful assistant for user questions.
instruction: Answer user questions to the best of your knowledge
```


Run the agent

```sh
# In web UI
adk web agents

# In terminal
adk run agents/basic_agent
```

More agent examples: https://github.com/search?q=repo%3Agoogle%2Fadk-python+path%3A%2F%5Econtributing%5C%2Fsamples%5C%2F%2F++language%3AYAML+_agent.yaml&type=code

### Intereact with the Agent

- Basic Agent
- Prime Agent (Tool Use)
- Learning Agent (Sub Agents)


## [AI Agent With Google Search](https://x.com/Saboo_Shubham_/status/1971038699329908885)

Adding Google Search tool is straightforward as ADK has built-in support for it.

```yaml
tools:
  - name: google_search
```

However, I found that there is no tool use inside the agent response in the web UI.

## [Research Agent with MCP Tools](https://x.com/Saboo_Shubham_/status/1971038699329908885)

Instead of using `firecrawl-mcp` tool, i switched to `brave-mcp` tool for web scraping and searching.

```yaml
tools:
  - name: MCPToolset
    args:
      stdio_server_params:
        command: "docker"
        args:
          - run
          - -i
          - --rm
          - -e
          - BRAVE_MCP_TRANSPORT
          - -e
          - BRAVE_API_KEY
          - mcp/brave-search
        env:
          BRAVE_MCP_TRANSPORT: "stdio"
          BRAVE_API_KEY: "${BRAVE_API_KEY}"
```

However, the environment variable using `BRAVE_API_KEY: "${BRAVE_API_KEY}"` does not seem to work I was expecting which is loading the API key from the `.env` file. Instead, the env variable inside the container is

```sh
$ env | grep BRAVE_API_KEY
BRAVE_API_KEY=${BRAVE_API_KEY}
```

To workaround this, I hardcoded the API key in the tool config as below:

```yaml
BRAVE_API_KEY: "******************************"
```

To obtain a API key go to : https://api-dashboard.search.brave.com/app/keys

## Challanges
- [ ] Deploy the Agent to Google Cloud Run
- [ ] Deploy the Agent to Vertex AI