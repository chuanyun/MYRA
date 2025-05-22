![MYRA](./MYRA.png "MYRA image")

# MYRA - MY mind-Reading Agent

**MYRA** is a multi-agent AI system that is personalized with user's preference in mind. 
It’s complexed enough to handle questions that chatGPT can not even do as it’s personalized for my preference! 

It is built using a set of LangChain/LangGraph agents in Nvidia AIQ toolkit with several custom and pre-built AI tools and workflows.


## Component Overview

In current **MYRA**, as time is limited, I only added 3 features - my daily ask of weather in a preferred location and stock news in Yahoo Finance, my favorite poems in my local collection, and general questions using Wikipedia. More to come!

Here are the 3 agents:
- **News Agent** – agent calling website query tool with my preferred location and news resource.
- **General Research Agent** – agent calling wikipedia tool.
- **Poem Agent** –  agent calling a RAG tool with my local files ingested.


LangChain and LangGraph is used to unify these agents into a single workflow as I like to control the routing more efficiently.


There is a supervisor agent that will assign/route incoming user query to one of the worker agents:

- (1) a `poem_react_agent` made out of `Langchain` via a `text_file_ingest` tool to ingest my local files.
- (2) a `news_agent` made out of `Langchian` via tools `website_query` and `current_datetime` to generate information from a provided website (url) at near real time.
- (3) a `wiki_agent` made out of `LangChain` with `wiki_search` as a tool to retrieve relevant contexts from wikipedia search for the given question.

the multi-agents architecture looks like the below

![LangGraph multi-agents workflow](./MyMCP_flow.png)

## Local Installation and Usage

If you have not already done so, follow the instructions in the [Install Guide](../docs/source/quick-start/installing.md#install-from-source) to create the development environment and install AIQ toolkit.

### Step 1: Set Your NVIDIA API Key 
If you have not already done so, follow the [Obtaining API Keys](../docs/source/quick-start/installing.md#obtaining-api-keys) instructions to obtain an NVIDIA API key. You need to set your NVIDIA API key as an environment variable to access NVIDIA AI services.

```bash
export NVIDIA_API_KEY=<YOUR_API_KEY>
```

### Step 2: Install the `text_file_ingestion` Workflow

**Install the `text_file_ingestion` Workflow**

```bash
uv pip install -e examples/documentation_guides/workflow/text_file_ingestion
```

### Step 3: Customize and Install the `multi_frameworks` Workflow

Check code change in examples/multi_frameworks/src/register.py especially for `router_prompt`. 

**Install the `multi_frameworks` Workflow**

```bash
uv pip install -e examples/multi_frameworks
```

### Step 4: Run the `multi_frameworks` Workflow

**Run the `multi_frameworks` Workflow**

note: the below is an example command to use and query this and trigger `wiki_agent`

```bash
aiq run --config_file=Mypersoo..../config.yml --input "list 5 dog breeds"
```

## Acknowledgements
- [Nvidia AIQToolkit](https://github.com/NVIDIA/AIQToolkit.git)
