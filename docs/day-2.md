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


## Challanges
- [ ] Deploy the Agent to Google Cloud Run
- [ ] Deploy the Agent to Vertex AI
- [ ] Deploy the Agent to AWS AgentCore.