[ Master Langchain v1 and Ollama - Chatbot, RAG and AI Agents](https://www.udemy.com/course/ollama-and-langchain/)

[Master LangGraph v1 and Ollama - Build Gen AI Agents](https://www.udemy.com/course/langgraph-with-ollama/)

## Section 1: Introduction

#### 1. Welcome & Course Overview

###### Object

- Build generative AI agents using LangGraph and Ollama.
- Learn how modern AI agent works

###### Overview

- Ollama
- LangChain
- LangGraph
  - Conditional Routing
  - ReAct Agent
    - Chain of Thought
    - Tree of Thought
  - Memory
    - Adapters
  - Guardrail, Interrupt and Human in the Loop
  - Reflection Agent
  - MCP Server

#### 3. Download Code Files & Install Requirements

GitHub: [LangGraph-and-Ollama](https://github.com/laxmimerit/LangGraph-and-Ollama)

## Section 2: Ollama Setup

#### 4. What is Ollama?

User can not directly talk with LLM, normally, `LLM Serving` and `API Provider` is needed.

`Ollama` take care of both LLM serving and APIs, so that you can access LLM by GUI or API calls.

#### 5. Exploring Ollama UI, Qwen3 and Gemma3 Models

Users can interact with LLM using GUI by simply clicking Ollama icon.

`qwen3`([Ollama Library](https://ollama.com/library/qwen3)) is a **thinking** model.

Capabilities: [Thinking](https://docs.ollama.com/capabilities/thinking)

#### 6. Context Window, Realtime Search & Runtime Settings

You can have a look at the following items in `Settings`

- Your account
- Expose Ollama to network
  - `localhost: 11434` is original port
- Model Location
- Context Length

#### 7. Fast Document Analysis Using Gemma3

Gemma3 ([Ollama Library](https://ollama.com/library/gemma3)) is a vision model, which means it accepts images alongside text so the model can describe, classify, and answer questions about what it sees.

Capabilities: [Vision](https://docs.ollama.com/capabilities/vision#vision)

#### 8. Deep Dive into Qwen3 Model

`qwen3:8b` model will be used in this course.

###### Model Architecture

Qwen3: [model](https://ollama.com/library/qwen3:8b/blobs/a3de86cd1c13)

###### Parameters

This is the default parameters of Qwen3.

```
{
    "repeat_penalty": 1,
    "stop": [
        "<|im_start|>",
        "<|im_end|>"
    ],
    "temperature": 0.6,
    "top_k": 20,
    "top_p": 0.95
}
```

#### 9. Qwen3 Benchmarking - Overview

Here shows how you can evaluate your model on various benchmarks.

[Qwen3](https://ollama.com/library/qwen3)

- GPQA: [A Graduate-Level Google-Proof Q&A Benchmark](https://github.com/idavidrein/gpqa)
- AIME25
- LiveCodeBench v6
- Arena-Hard v2
- BFCL-v3

#### 10. Run Local Benchmark Tests with Qwen3

(skipped)

#### 11. How to Choose the Right Model for Any Task

[Ollama](https://ollama.com/search) has the following tags:

- `cloud`: models hosted in the cloud
- `embedding`: Embedding Models
- `vision`: Models that can deal with images along with texts
- `tools`: Models that supports function calling
- `thinking`: Models that separates their reasoning trace from the final answer.

#### 12~19. Ollama Basics And Advanced Usage

(skipped)

## Section 3: LangChain Getting Started

#### 20. LangSmith Setup for Debugging & Tracing

`LangChain` is the **fundamentals** of LangGraph.

1. Install `langchain-core` [here](https://reference.langchain.com/python/langchain-core):

   ```bash
   uv add langchain-core
   ```

2. Install [Ollama intergrations](https://reference.langchain.com/python/integrations/overview): `langchain-ollama`

   ```bash
   uv add langchain-ollama
   ```

3. Install other library

   ```bash
   uv add dotenv
   ```

`LangSmith` is AI observability tool, see [LangSmith](https://smith.langchain.com/).

In LangSmith, we could

- Create a project

- Create an api-key (Settings -> API Key)

- Set up environment variables

  ```
  LANGSMITH_TRACING=true
  LANGSMITH_ENDPOINT=https://api.smith.langchain.com
  LANGSMITH_API_KEY=<your-api-key>
  LANGSMITH_PROJECT="test"
  ```

#### 21. Open-Source Tracing Tools: LangFuse & Opik

LangFuse: [Open Source LLM Engineering Platform](https://langfuse.com/)

Opik: [Open-source AI Observability, Evaluation, and Optimization](https://github.com/comet-ml/opik)

MLflow: [Tracing QuickStart](https://mlflow.org/docs/latest/genai/tracing/quickstart/)

#### 22. Getting Started with ChatOllama + Gemma3

LangChain: [Integrations](https://reference.langchain.com/python/integrations/overview)

`ChatOllama` is the key to interact with Ollma models, see [ChatOllama](https://reference.langchain.com/python/langchain-ollama/chat_models/ChatOllama).

```python
from langchain_ollama import ChatOllama

llm = ChatOllama(
    model="gemma3:1b",
    base_url="http://localhost:11434",
    temperature=0.7,
    num_predict=1024,
    num_ctx=2048
)
```

> model='gemma3:1b' num_ctx=2048 num_predict=1024 temperature=0.7 base_url='http://localhost:11434'

#### 23. Generate Responses & Trace in LangSmith

LangChain: [Messages](https://reference.langchain.com/python/langchain/messages)

###### Messages

There are three `Messages` in LangChain:

- System Message
- Human Message
- AI Message

LangChain uses three different classes to manage messages: `SystemMessage`, `HumanMessage` and `AIMessage`.

Developers can assign `content` to each message, then LangChain will append `additional_kwargs` and `response_metadata` automatically.

```python
from langchain_core.messages import SystemMessage, HumanMessage, AIMessage

messages = [
    SystemMessage(content="You are a helpful assistant"),
    HumanMessage(content="What is LangChain?")
]

```

> [SystemMessage(content='You are a helpful assistant', additional_kwargs={}, response_metadata={}), HumanMessage(content='What is LangChain?', additional_kwargs={}, response_metadata={})]

In addition, LLM's response will be `AIMessage` class, for example, the following message is returned after `llm.invoke()`

Note that `response_metadata` is created by AI automatically

```python
response = llm.invoke(input=messages)
print(response)
```

> content='Okay, let\'s break down LangChain – it’s a really interesting and rapidly growing tool for building applications powered by large language models (LLMs). \*\*\*)' additional_kwargs={} response_metadata={'model': 'gemma3:1b', 'created_at': '2026-xx-xxTxx:xx:xx.xx', 'done': True, 'done_reason': 'stop', 'total_duration': 1022xx, 'load_duration': 939xx, 'prompt_eval_count': 24, 'prompt_eval_duration': 233xx, 'eval_count': 8xx, 'eval_duration': 881xx, 'logprobs': None, 'model_name': 'gemma3:1b', 'model_provider': 'ollama'} id='lc_run--xx' tool_calls=[] invalid_tool_calls=[] usage_metadata={'input_tokens': 24, 'output_tokens': 813, 'total_tokens': 837}

###### Observability: LangSmith

Now, we should be able to see execution details in LangSmith Project.

#### 24. Using ChatPromptTemplate

LangChain Core: [Prompts](https://reference.langchain.com/python/langchain-core/prompts)

`ChatPromptTemplate` helps developer to format messages more easily, see [reference](https://reference.langchain.com/python/langchain-core/prompts/chat/ChatPromptTemplate).

It is also a langchain runnable (which can be executed by `invoke`), so it can be

```python
from langchain_core.prompts import ChatPromptTemplate

prompt = ChatPromptTemplate(
    [
        ("system", "You are expert in {subject}. Explain it to a {audience} students"),
        ("human", "Can you explain {topic}?")
    ]
)

messages = prompt.invoke(input={
    "subject": "Physics",
    "audience": "high school",
    "topic": "Quantum Mechanics"
})

print(messages)

# response = llm.invoke(input=messages)
# response.pretty_print()
```

We can notice that `ChatPromptTemplate` format messages list for us, with changeable parts filled in.

> messages=[SystemMessage(content='You are expert in Physics. Explain it to a high school students', additional_kwargs={}, response_metadata={}), HumanMessage(content='Can you explain Quantum Mechanics?', additional_kwargs={}, response_metadata={})]

#### 25. Building Chains with Runnables

LangChain Core: [Runnables](https://reference.langchain.com/python/langchain-core/runnables)

In Lesson 24, we can see that `invoke` method are executed twice, once in prompting, and once in LLM calling.

In LangChain, we can chain these together.

- Note that every class that have an `invoke` method is LangChain runnable
- Every LangChain `runnable` can be chained together, in which the output (return value) will be input of the next item on chain

```python
# Both prompt (ChatPromptTemplate) and llm (ChatOllama) has invoke method
chain = prompt | llm

# The input will be passed to prompt
# And the output of prompt (formatted messages) will be the input argument of invoke of llm
response = chain.invoke(input={
    "subject": "Physics",
    "audience": "high school",
    "topic": "Quantum Mechanics"
    })

response.pretty_print()
```

#### 26. Format Outputs with StrOutputParser

LangChain Core: [OutputParser](https://reference.langchain.com/python/langchain-core/output_parsers)

`Output Parser` can be used to parse the results of response from LLM.

`StrOutputParser` will convert response to a plain string.

```python
parser = StrOutputParser()
chain = prompt | llm | parser

response = chain.invoke(input={
    "subject": "Physics",
    "audience": "high school",
    "topic": "Quantum Mechanics"
    })

# Note that here response is plain str
print(response)
```

#### 27. Streaming Response and Structured Outputs (Pydantic)

###### Structured Output

LangChain: [with_structured_output](https://reference.langchain.com/python/langchain/chat_models/base/_ConfigurableModel/with_structured_output)

Note that structured output should be **binding** to a LLM model, using `with_structured_output` method.

```python
class Sentiment(BaseModel):
    sentiment: bool = Field(..., description="True if the sentiment is positive, False otherwise")
    reasoning: str = Field(..., description="A brief explanation of the sentiment.")


structured_llm = llm.with_structured_output(Sentiment)
response = structured_llm.invoke("I love programming!")
```

> sentiment=False reasoning="That's fantastic! Programming is a really rewarding and complex field. It's awesome that you love it! What specifically do you enjoy about it? Knowing a bit more about your interests could be fun to talk about. 😊"

###### Streaming

By using `stream` instead of `invoke`, we can achieve streaming in LLM's response.

- `stream` method returns an `Iterator`
- Specifiy `end` and `flush` parameter helps to make response streaming.

```python
for chunk in structured_llm.stream("I love programming!"):
    print(chunk, end="", flush=True)
```

## Section 4: LangGraph Getting Started

#### Section Summary:

```python
from typing import TypedDict
from langgraph.graph import StateGraph, START, END

# Define State Schema
class SimpleState(TypedDict):
    input_text: str
    output_text: str

# Define Nodes
def process_input(state: SimpleState) -> SimpleState:
    output_text = state["input_text"].upper()
    return {"output_text": output_text}

def add_prefix(state: SimpleState) -> SimpleState:
    output_text = "Hey, I have added something here, " + state["output_text"]
    return {"output_text": output_text}

def add_suffix(state: SimpleState) -> SimpleState:
    output_text = state["output_text"] + ". And here I added suffix"
    return {"output_text": output_text}


def create_simple_graph():
    builder = StateGraph(SimpleState)

    # add the nodes
    builder.add_node("process_input",process_input)
    builder.add_node("add_prefix", add_prefix)
    builder.add_node("add_suffix", add_suffix)

    # connect the edges
    builder.add_edge(START, "process_input")
    builder.add_edge("process_input","add_prefix")
    builder.add_edge("add_prefix","add_suffix")
    builder.add_edge("add_suffix",END)

    graph = builder.compile()

    return graph

# Create and Invoke Graph
graph = create_simple_graph()

initial_state = SimpleState(input_text="John")
response = graph.invoke(initial_state)

print(response)
```

#### 28. Flow Engineering & FSM Concepts

LangGraph: [Overview](https://reference.langchain.com/python/langgraph)

###### Flow Engineering and Finite State Machine

LangGraph is a **low-level** `orchestration` framework for building stateful, multi-agent applications. Think of it as a way to create **workflows** where each step (node) processes data and passes it to the next step.

- State: Shared memory that all node can read from and write to
  - Usually `TypedDict`
  - Storing messages like: `{messages: [h1, m1, m2]}`
- Nodes: Functions that do specific tasks (like process data)
  - Any graph starts from `__start__` and end at `__end__`
  - There are built-in nodes like `__start__` and `__end__`
- Edges: Connections between nodes that define the flow
  - Can add conditional rules

#### 29. Creating Custom State in LangGraph

LangGraph: [Graph - StateGraph, START, END](https://reference.langchain.com/python/langgraph/graph)

`StateGraph` is like a canvas, which gather all nodes and edges together.

- StateGraph needs to be `compiled` before using.
- A Graph can exclude LLM-related parts and only contain functions
- Each node is a self-defined function with `state` passed through

```python
from typing import TypedDict
from langgraph.graph import StateGraph

class SimpleState(TypedDict):
    input_text: str
    output_text: str
```

#### 30. Custom Node Creation + State Mutation

A `Custom Node` is nothing more than a Python function, which

- Takes `state` as argument
  - State is no more than a dictionary (TypedDict)
  - All Keys can be accessed in each node's function.
- Return `state`
  - Note that LangGraph will take care of your state
  - Even if you only return one key, LangGraph will still keep other keys in the state

```python
def process_input(state: SimpleState) -> SimpleState:
    output_text = state["input_text"].upper()

    # Note that here, LangGraph will take care of other keys
    return {"output_text": output_text}
```

#### 31. Working with Nested Nodes

Here, we can define our next node. Similarily, it will take `state` as an argument and then return state (part of it).

```python
def add_prefix(state: SimpleState) -> SimpleState:
    output_text = "Hey, I have added something here, " + state["output_text"]
    return {"output_text": output_text}

def add_suffix(state: SimpleState) -> SimpleState:
    output_text = state["output_text"] + ". And here I added suffix"
    return {"output_text": output_text}
```

###### Simulating Workflows in LangGraph

Then, let's simulate workflows in LangGraph. Basiclly, the next node takes state form the former one and process it.

```python
state = SimpleState(input_text="John", output_text="")

response = add_suffix(state=add_prefix(state=process_input(state=state)))
print(response)
```

Because now we do not use `LangGraph`, so we will only get `output_text` here. LangGraph will return all keys in state in the future.

> {'output_text': 'Hey, I have added something here, JOHN. And here I added suffix'}

#### 32. Build & Visualize Your First LangGraph

`StateGraph` will be the **canvas** of our workflow.

- StateGraph will take our custom TypedDict as `state_schema` and take care of it
- `add_node`, `add_edge` and `add_conditional_edge` is used to add and link nodes
  - `add_node` need two arguments: node name and node function
- StateGraph needs to be `compile` so it can return a **runnable graph**

```python
def create_simple_graph():
    builder = StateGraph(SimpleState)

    # add the nodes
    builder.add_node("process_input",process_input)
    builder.add_node("add_prefix", add_prefix)
    builder.add_node("add_suffix", add_suffix)

    # connect the edges
    builder.add_edge(START, "process_input")
    builder.add_edge("process_input","add_prefix")
    builder.add_edge("add_prefix","add_suffix")
    builder.add_edge("add_suffix",END)

    # make it langChain runnable
    graph = builder.compile()

    return graph

graph = create_simple_graph()
```

#### 33. Invoke Graph & Inspect State Updates

After `compilling` your canvas, which is `StateGraph`, it has become a LangChain `runnable` and can be `invoke` thereafter.

Before invoking your graph, make sure the **state** you passed contains all the key graph nodes need.

```python
initial_state = SimpleState(input_text="John")

response = graph.invoke(initial_state)
print(response)
```

Note that since LangGraph takes care of our state (by passing state schema to canvas), we now have both keys returned

> {'input_text': 'John', 'output_text': 'Hey, I have added something here, JOHN. And here I added suffix'}

## Section 5: Conditional Routing

In this section, we will learn:

- Integrate LLMs into LangGraph workflows
- Use Pydantic BaseModel for structured output
- Inplement conditional routing based on sentiment

#### Section Summary: Code

```python
from typing import TypedDict, Literal
from langgraph.graph import StateGraph, START, END
from langchain_ollama import ChatOllama
from langchain_core.messages import SystemMessage, HumanMessage
from pydantic import BaseModel, Field

# Configuration
BASE_URL = "http://localhost:11434"
MODEL_NAME = "deepseek-r1"

llm = ChatOllama(model=MODEL_NAME, base_url=BASE_URL)


class SentimentAnalysis(BaseModel):
    sentiment: Literal["positive","negative"] = Field(description="The sentiment classification either positive or negative")
    confidence: float = Field(ge=0, le=1.0, description="Confidence score from 0.0 to 1.0")
    reason: str = Field(description="Brief explanation")

structured_llm = llm.with_structured_output(schema=SentimentAnalysis)

class SentimentState(TypedDict):
    original_tweet: str
    # LLM will assign sentiment (positive or negative) here
    sentiment: str
    confidence: float
    response_tweet: str

def analyze_sentiment(state:SentimentState):
    tweet = state["original_tweet"]
    print(f"Analyzing customer tweet: {tweet}")         # for debug usage

    messages = [
        SystemMessage("Analyze sentiment and provide the structured output. Use 0 to 1.0 scale for confidence. Lower is nagative and higher is positive"),
        HumanMessage(tweet)
    ]
    analysis = structured_llm.invoke(messages)

    print(f"Sentiment Analysis is done \n{analysis}")   # for debug usage

    return {"sentiment": analysis.sentiment,
            "confidence": analysis.confidence}

def generate_positive_response(state: SentimentState):

    print(f"current state in positive response node: {state}")  # for debug usage

    messages = [
        SystemMessage(f"""Generate a warm response to this positive tweet under 280 chars.
                      Confidence: {state["confidence"]} High confidence means being enthusiastic otherwise being friendly"""),
        HumanMessage(state["original_tweet"])
    ]

    response = llm.invoke(messages)
    return {"response_tweet": response.content.strip()}


def generate_negative_response(state: SentimentState):

    print(f"current state in negative response node: {state}")  # for debug usage

    messages = [
        SystemMessage(f"""Generate and empathetic response to this negative tweet under 280 chars.
                      If confidence {state["confidence"]} is very low then be empathetic, otherwise be understanding"""),
        HumanMessage(state["original_tweet"])
    ]

    response = llm.invoke(messages)
    return {"response_tweet": response.content.strip()}

def route_by_sentiment(state: SentimentState):
    if state["sentiment"] == "positive":
        return "positive_response"
    else:
        return "negative_response"

def create_router_graph():
    # Get canvas for graph
    builder = StateGraph(SentimentState)

    # Add nodes
    builder.add_node("analyze", analyze_sentiment)
    builder.add_node("positive_response", generate_positive_response)
    builder.add_node("negative_response", generate_negative_response)

    # Connect nodes
    builder.add_edge(START, "analyze")
    builder.add_conditional_edges("analyze", route_by_sentiment, ["positive_response", "negative_response"])
    builder.add_edge("positive_response", END)
    builder.add_edge("negative_response", END)

    # Make canvas runnable
    graph = builder.compile()

    return graph

graph = create_router_graph()

result = graph.invoke({"original_tweet": "Just launched my new project! The response from everyone has been amazing so far!"})

print(f"Response from LLM:{result["response_tweet"]}")
```

#### 34. What is Conditional Routing in LangGraph

Previously, we have built a linear graph. In this section, we will add conditional edges, in which condition is evaluated be an LLM node.

###### Visualization of Conditional Routing

```
                __start__
                    |
                    v
         +----------------------+
         |  Sentiment Analyser  |
         |       (Router)       |
         +----------------------+
                    |
            +-------+-------+
            |               |
       (Positive)       (Negative)
            |               |
            v               v
+------------------+  +------------------+
| Positive         |  | Negative         |
| Sentiment Node   |  | Sentiment Node   |
+------------------+  +------------------+
            \               /
             \             /
              \           /
                   v
                 __END__
```

###### Preparation

```python
from typing import TypedDict, Literal
from langgraph.graph import StateGraph, START, END
from langchain_ollama import ChatOllama
from langchain_core.messages import SystemMessage, HumanMessage
from pydantic import BaseModel, Field

# Configuration
BASE_URL = "http://localhost:11434"
MODEL_NAME = "deepseek-r1"
llm = ChatOllama(model=MODEL_NAME, base_url=BASE_URL)
```

#### 35. Create Pydantic Model for Sentiment Classification

Because we rely on LLM to provide judgment, a more structured output is preferred.

Here, we can use `Pydantic` to enforce LLM to choose from two options only: `possitive` and `negative`.

```python
class SentimentAnalysis(BaseModel):
    sentiment: Literal["positive","negative"] = Field(description="The sentiment classification either positive or negative")
    confidence: float = Field(ge=0, le=1.0, description="Confidence score from 0.0 to 1.0")
    reason: str = Field(description="Brief explanation")

# Bind schema to LLM
structured_llm = llm.with_structured_output(schema=SentimentAnalysis)
```

#### 36. Designing Sentiment State for Tweet Replies

```python
class SentimentState(TypedDict):
    original_tweet: str
    # LLM will assign sentiment (positive or negative) here
    sentiment: str
    confidence: float
    response_tweet: str
```

#### 37. Writting Sentiment Analysis Node

In this node, we use llm which is equipped with structured output.

- Read user's input, `original_tweet` from state
- Wrap instructions and user input into `messages` and invoke LLM
- Return the output to state

```python
def analyze_sentiment(state:SentimentState):
    tweet = state["original_tweet"]
    print(f"Analyzing customer tweet: {tweet}")         # for debug usage

    messages = [
        SystemMessage("Analyze sentiment and provide the structured output. Use 0 to 1.0 scale for confidence. Lower is nagative and higher is positive"),
        HumanMessage(tweet)
    ]
    analysis = structured_llm.invoke(messages)

    print(f"Sentiment Analysis is done \n{analysis}")   # for debug usage

    return {"sentiment": analysis.sentiment,
            "confidence": analysis.confidence}
```

> Analyzing customer tweet: Just launched my new project!
> Sentiment Analysis is done
> sentiment='positive' confidence=0.85 reason="The statement expresses excitement about a new achievement ('launched my new project')."

#### 38. Positive Tweet Handler Node

This node:

- Read the output of sentiment analyzer (stored in state)
- Use LLM to generate response based on the sentiment and confidence
- Return LLM response (content only)

```python
def generate_positive_response(state: SentimentState):

    print(f"current state in positive response node: {state}")  # for debug usage

    messages = [
        SystemMessage(f"""Generate a warm response to this positive tweet under 280 chars.
                      Confidence: {state["confidence"]} High confidence means being enthusiastic otherwise being friendly"""),
        HumanMessage(state["original_tweet"])
    ]

    response = llm.invoke(messages)
    return {"response_tweet": response.content.strip()}
```

#### 39. Negative Tweet Handler + Route Node

```python
def generate_negative_response(state: SentimentState):

    print(f"current state in negative response node: {state}")  # for debug usage

    messages = [
        SystemMessage(f"""Generate and empathetic response to this negative tweet under 280 chars.
                      If confidence {state["confidence"]} is very low then be empathetic, otherwise be understanding"""),
        HumanMessage(state["original_tweet"])
    ]

    response = llm.invoke(messages)
    return {"response_tweet": response.content.strip()}
```

###### Router Node

The router deside to which direction the flow will go.

- Router function only returns string
- However, the string must **match** with the name of the next node it points at.
- Router function will **NOT** be included as a node, but an **edge**

```python
def route_by_sentiment(state: SentimentState):
    if state["sentiment"] == "positive":
        return "positive_response"
    else:
        return "negative_response"
```

#### 40. Build Complete Sentiment Graph

Here, router node is added as `conditional edge`.

```python
def create_router_graph():
    # Get canvas for graph
    builder = StateGraph(SentimentState)

    # Add nodes
    builder.add_node("analyze", analyze_sentiment)
    builder.add_node("positive_response", generate_positive_response)
    builder.add_node("negative_response", generate_negative_response)

    # Connect nodes
    builder.add_edge(START, "analyze")
    builder.add_conditional_edges("analyze", route_by_sentiment, ["positive_response", "negative_response"])
    builder.add_edge("positive_response", END)
    builder.add_edge("negative_response", END)

    # Make canvas runnable
    graph = builder.compile()

    return graph

graph = create_router_graph()
```

#### 41. Run Sentiment Analyzer + Tweet Generator

```python
graph = create_router_graph()

result = graph.invoke({"original_tweet": "Just launched my new project! The response from everyone has been amazing so far!"})

print(f"Response from LLM:{result["response_tweet"]}")
```

Note here graph returns `state` in the end.

> Analyzing customer tweet: Just launched my new project! The response from everyone has been amazing so far!
> Analyzing customer tweet: Just launched my new project! The response from everyone has been amazing so far!
> Sentiment Analysis is done
> sentiment='positive' confidence=0.9 reason="The text expresses excitement about a new project launch and uses the word 'amazing' to describe the response, indicating strong positive sentiment with high certainty."
> current state in positive response node: {'original_tweet': 'Just launched my new project! The response from everyone has been amazing so far!', 'sentiment': 'positive', 'confidence': 0.9}
> Response from LLM:Awesome news! So excited for everyone to love it too! Can't wait to see where this amazing response takes you!

## Section 6: LangGraph ReAct Agent

#### Section Summary: Code

###### Architecture

```
                  +-------------+
                  |  __start__  |
                  +-------------+
                        |
                        v
                +----------------+
                |       LLM      |
                +----------------+
                 |    |       |
        (call tool)   |   	(finish)
                 |    |       |
                 v    |       v
           +------------+     |
           |    Tool    |     |
           +------------+     |
                              |
                           		|
                            	|
                          		|
                           		|
                           		v
                        +-------------+
                        |   __end__   |
                        +-------------+
```

###### Code

```python
import operator
import requests
from dotenv import load_dotenv
from typing import TypedDict, Annotated

from langchain_ollama import ChatOllama
from langgraph.graph import StateGraph, START, END
from langgraph.prebuilt import ToolNode
from langchain_core.tools import tool
from langchain_core.messages import SystemMessage, HumanMessage


# Load environment variables from .env file, so that LangSmith tracing is enabled.
load_dotenv()

# Configuration for Ollama server and model
BASE_URL = "http://localhost:11434"
MODEL_NAME = "qwen3:8b"

llm = ChatOllama(model=MODEL_NAME, base_url=BASE_URL)

# Define the state schema for the agent. The state will keep track of the conversation messages.
class AgentState(TypedDict):
    messages: Annotated[list, operator.add]

# Define a tool for getting weather information.
@tool
def get_weather(location: str) -> dict:
    """Get current weather for a location.

    Use for queries about weather, temperature, or conditions in any city.
    Examples: "weather in Paris", "temperature in Tokyo", "is it raining in London"

    Args:
        location: City name (e.g., "New York", "London", "Tokyo")

    Returns:
        Current weather information including temperature and conditions.
    """

    # In a real implementation, you would call an actual weather API here.
    # url = f"https://wttr.in/{location}?format=j1"
    # response = requests.get(url=url, timeout=10)
    # response.raise_for_status()
    # data = response.json()

    # hard-coding because wttr.in is down
    weather_data = {
        "location": location,
        "weather": "rainy, but rain will stop in 2 hours."}

    return weather_data


# Define agent node
def agent_node(state: AgentState):
    # Bind tools to the LLM, so that it can call tools during generation.
    llm_with_tools = llm.bind_tools(tools=[get_weather])

    messages = state["messages"]
    response = llm_with_tools.invoke(messages)

    # AIMessages will contain tool_calls attributes during tool call turn
    if hasattr(response, "tool_calls") and response.tool_calls:
        for tc in response.tool_calls:
            print(f"This agent called tool: {tc.get("name", "?")} with args: {tc.get("args", "?")}")
    else:
        print(f"[AGENT] generating responses...")

    # The value of messages should be list, because of operator.add
    return {"messages": [response]}


# Define the routing function
def should_continue(state:AgentState):
    last_message = state["messages"][-1]

    if hasattr(last_message, "tool_calls") and last_message.tool_calls:
        return "tools"      # This key should be the same with tool node
    else:
        return END


# Build the agent graph
def create_agent():
    # Get graph canvas
    # The canvas should accept state schema, instead of state instance
    builder = StateGraph(state_schema=AgentState)

    builder.add_node("agent", agent_node)
    builder.add_node("tools", ToolNode(tools=[get_weather])) # Should be the same with that in routing

    builder.add_edge(START, "agent")
    builder.add_conditional_edges(source="agent", path=should_continue, path_map=["tools", END])
    builder.add_edge("tools", "agent")  # Do not forget to connect tool node back to agent

    graph = builder.compile()

    return graph

# Create the agent
agent = create_agent()

# Test the agent with a weather query.
query = "What is the weather in LA and new york??"
inital_state = AgentState(
    messages=[SystemMessage("You are a helpful assistant with tools to check weather and report to the user."),
              HumanMessage(query)]
)

#Invoke the agent with the initial state
result = agent.invoke(inital_state)
result["messages"][-1].pretty_print()
```

###### Results

> This agent called tool: get_weather with args: {'location': 'LA'}
> This agent called tool: get_weather with args: {'location': 'New York'}
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> The weather in Los Angeles is currently rainy, but the rain will stop in 2 hours. Similarly, New York is also experiencing rain, with the same forecast of no rain in 2 hours. Let me know if you need further details!

#### 42. Chain of Thought (CoT) and Tree of Thought (ToT) Design Pattern

(Skipped)

#### 43. ReAct Pattern - Reason + Act Pipeline

LangChain: [Example of ReAct Loop](https://docs.langchain.com/oss/python/langchain/agents#example-of-react-loop)

#### 44. State Management for Agents

Thinking in LangGraph: [Design Your State](https://docs.langchain.com/oss/python/langgraph/thinking-in-langgraph#step-3-design-your-state)

`State` is crutial for an agent. At the very beginning, only `HumanMessage` is passed, and as our graph being executed, `AIMessage` and message about Tool Calling will be automatically appended to it.

- `State` should contain `messages` field, which is a list of message.
  - `messages = [h1] -> [h1, AI1, ...]`
- `messages` should be **Annotated**

#### 45. Create AgentState with Reducers

###### Configuration

```python
from langgraph.graph import StateGraph, START, END
from langchain_ollama import ChatOllama
from langchain_core.messages import SystemMessage, HumanMessage

# Configuration
BASE_URL = "http://localhost:11434"
MODEL_NAME = "qwen3"

llm = ChatOllama(model=MODEL_NAME, base_url=BASE_URL)
```

###### Create AgentState

**Important**:

- `Annotated` must be used to tag metadata to `messages`,
  - This is in order to let framework read and automatically **append** messages, instead of overwriting it.
  - When functions (nodes) return `messages`, it will be automatically appended in `messages` list.

- `operator` convert calculations like `+` to function.

```python
import operator
from typing import TypedDict, Annotated

class AgentState(TypedDict):
    messages: Annotated[list, operator.add]
```

###### ToolNode

LangChain: [ToolNode](https://docs.langchain.com/oss/python/langchain/tools#toolnode)

`ToolNode` is a prebuilt node that executes tools in LangGraph workflows. It handles parallel tool execution, error handling, and state injection automatically.

```python
from langgraph.prebuilt import ToolNode
```

#### 46. Build Weather Tool (Realtime API)

###### Tools

LangChain: [Create Tools](https://docs.langchain.com/oss/python/langchain/tools#create-tools)

Tools in LangChain/LangGraph is no more than a **function** that is decoratored by `@tool`.

- Note that decorator `@tool` will turn a function to a `Runable`
- So that you can `invoke` this tool.

- By default, the function’s docstring becomes the tool’s description that helps the model understand when to use it

###### Tool Samples

Free Weather API: [wttr.in](https://github.com/chubin/wttr.in)

```python
@tool
def get_weather(location: str) -> str:
    """Get current weather for a location.

    Use for queries about weather, temperature, or conditions in any city.
    Examples: "weather in Paris", "temperature in Tokyo", "is it raining in London"

    Args:
        location: City name (e.g., "New York", "London", "Tokyo")

    Returns:
        Current weather information including temperature and conditions.
    """
    url = f"https://wttr.in/{location}?format=j1"
    # response = requests.get(url=url, timeout=10)

    # response.raise_for_status()
    # data = response.json()

    # hard-coding because wttr.in is down
    data = {
        "location": location,
        "weather": "rainy, but rain will stop in 2 hours."}

    return data
```

###### Tool Invocation

Note that `get_weather` is wrapped as a `tool`, instead of a Python function.

So, a dictionary or parameters and its arguments should be passed here.

```python
# get_weather("LA") will not work
weather_in_LA = get_weather.invoke({"location": "LA"})
print(weather_in_LA)
```

> {'location': 'LA', 'weather': 'rainy, but rain will stop in 2 hours.'}

#### 47. Use wttr.in + Build Calculation Tool

(skipped)

#### 48. Test Weather & Calculation Tool

(Skipped)

#### 49. Create Agent Node

`bind_tools` method is used here to bind tools to LLM.

- LLM will read the **docstring** of tools (funtions) and generate arguments in dictionary format if necessary
- During tool calling turn, LLM will return `AIMessage` with `tool_calls` attributes.
- LLM can call multiple tools in one turn

```python
def agent_node(state: AgentState):
    llm_with_tools = llm.bind_tools(tools=[get_weather])

    messages = state["messages"]

    response = llm_with_tools.invoke(messages)

    # AIMessages will contain tool_calls attributes during tool call turn
    if hasattr(response, "tool_calls") and response.tool_calls:
        for tc in response.tool_calls:
            print(f"This agent called tool: {tc.get("name", "?")} with args: {tc.get("args", "?")}")
    else:
        print(f"[AGENT] generating responses...")

    # The value should be list, because of operator.add
    return {"messages": [response]}
```

###### Test LLM Tool Call

```python
inital_state = AgentState(
    messages=[SystemMessage("You are a helpful assistant with a tool to help user to know the weather"),
              HumanMessage("Please tell me the weather in LA")]
)

results = agent_node(state=inital_state)
print(type(results), f"Agent Node returns as the follows:\n{results}")
```

In this example, LLM calls `get_wather` twice, and return `name` and `args` separately.

> This agent called tool: get_weather with args: {'location': 'Los Angeles'}
> This agent called tool: get_weather with args: {'location': 'New York'}
>
> <class 'dict'>
>
> Agent Node returns as the follows:
>
> {'messages': [AIMessage(content='', additional_kwargs={}, response_metadata={'model': 'qwen3:8b', 'created_at': '2026-xx-xxTxxxxZ', 'done': True, 'done_reason': 'stop', 'total_duration': 130xx, 'load_duration': 20xx, 'prompt_eval_count': 2xx, 'prompt_eval_duration': 130xx, 'eval_count': 1xx, 'eval_duration': 96xx, 'logprobs': None, 'model_name': 'qwen3:8b', 'model_provider': 'ollama'}, id='lc_run--xx', **tool_calls=[{'name': 'get_weather', 'args': {'location': 'Los Angeles'}, 'id': 'c9xx', 'type': 'tool_call'}, {'name': 'get_weather', 'args': {'location': 'New York'}, 'id': '0exx', 'type': 'tool_call'}]**, invalid_tool_calls=[], usage_metadata={'input_tokens': 2xx, 'output_tokens': 1xx, 'total_tokens': 4xx})]}

#### 50. Debug Tool Calls Inside Agents

(skipped)

#### 51. Add Conditional Tool Execution

After LLM calling, graph runtime will decide if it should call tools, or goes to the `END` and return state to user.

```python
def should_continue(state:AgentState):
    last_message = state["messages"][-1]

    if hasattr(last_message, "tool_calls") and last_message.tool_cals:
        # This key should be the same with tool node
        return "tools"
    else:
        return END
```

#### 52. Build Full ReAct Agent

In this lesson, we finally link the node together and compile the graph.

```python
def create_agent():
    # Get graph canvas
    # The canvas should accept state schema, instead of state instance
    builder = StateGraph(state_schema=AgentState)

    builder.add_node("agent", agent_node)
    builder.add_node("tools", ToolNode(tools=[get_weather])) # Should be the same with that in routing

    builder.add_edge(START, "agent")
    builder.add_conditional_edges(source="agent", path=should_continue, path_map=["tools", END])
    builder.add_edge("tools", "agent")  # Do not forget to connect tool node back to agent

    graph = builder.compile()

    return graph
```

#### 53. ReAct Agent in Action - Output & States

```python
agent = create_agent()				# Create the agent instance (configured with tools, e.g., weather tool)
query = "What is the weather in LA?"	# Define the user query

# Initialize the agent state with conversation history
initial_state = AgentState(
    messages=[
        # System prompt: defines the assistant's role and available tools
        SystemMessage(
            "You are a helpful assistant with tools to check weather and report to the user."
        ),
        # User message: actual question from the user
        HumanMessage(query)
    ]
)

result = agent.invoke(initial_state)	# Invoke the agent with the initial state
result["messages"][-1].pretty_print()	# Print the assistant's final response message
```

###### Responses from ReAct Agent

Agent in LangGraph will take state in and return state. So, we have a dictionary in the end with `messages` key and a list of `SystemMessage`, `AIMessage`, `HumanMessage`.

> This agent called tool: get_weather with args: {'location': 'Los Angeles'}
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> The current weather in Los Angeles is rainy, but the rain is expected to stop within the next 2 hours. You might want to keep an umbrella handy for now, but conditions should improve soon!

## Section 7: Agentic Memory and Streaming

LangGraph: [Persistence](https://docs.langchain.com/oss/python/langgraph/persistence)

In this section, we will learn to build a stateful agent.

#### Learning Objectives

- Implement conversation memory with `checkpointers`
- Use `thread_id` for multiple conversations
- `Stream` response from real-time UX

#### 55. Understanding Agentic Memory

In previous section, our agent only remembers chat history of a certain invocation.

That agent will lose all information when terminated.

In this section, we will create a memory layer for our agent.

The memory can be stored in a database, for example `sqlite` or `postgresql`.

#### 56. Notebook Setup

In this section, the same agent will be used.

LangGraph: [Add Short-Term Memory](https://docs.langchain.com/oss/python/langgraph/add-memory#add-short-term-memory)

```python
# Use RAM by default
from langgraph.checkpoint.memory import MemorySaver
```

#### 57. Agent Node with Tools

(Skipped)

#### 58 & 59. ReAct Agent with MemorySaver - Demo

###### Build Agent

- To equip our agent with short-term memory, we need:
  - Pass `InMemorySaver` as `checkpointer` when compiling the graph
  - Specify a `thread_id` when invoking the agent
    - The `thread_id` should be provided via the `configurable` argument

```python
# Build the agent graph
def create_agent():
    # Get graph canvas
    # The canvas should accept state schema, instead of state instance
    builder = StateGraph(state_schema=AgentState)
    memory = InMemorySaver()

    builder.add_node("agent", agent_node)
    builder.add_node("tools", ToolNode(tools=[get_weather])) # Should be the same with that in routing

    builder.add_edge(START, "agent")
    builder.add_conditional_edges(source="agent", path=should_continue, path_map=["tools", END])
    builder.add_edge("tools", "agent")  # Do not forget to connect tool node back to agent

    graph = builder.compile(checkpointer=memory)

    return graph
```

###### Test Agent

```python
# Configure thread id
config = {"configurable" :{"thread_id": "react-agent-building-demo"}}

# ========== First Run ===========================
# Test the agent with a weather query.
query = "What is the weather in LA and new york??"
inital_state = AgentState(
    messages=[SystemMessage("You are a helpful assistant with tools to check weather and report to the user."),
              HumanMessage(query)]
)

#Invoke the agent with the initial state
result_first_turn = agent.invoke(inital_state, config=config)
result_first_turn["messages"][-1].pretty_print()

# ========== Second Run ===========================
review_query = "What topic did the agent just discuss with the user? Did it call any tools? If so, which ones and what were the arguments?"
cont_state = AgentState(
    messages=[HumanMessage(review_query)]
)

# Here, messages (list) in cont_state will be added to initial_state
# So, agent will know what happened in the first run
result_second_turn = agent.invoke(cont_state, config=config)
result_second_turn["messages"][-1].pretty_print()
```

> This agent called tool: get_weather with args: {'location': 'LA'}
> This agent called tool: get_weather with args: {'location': 'New York'}
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> The weather in both locations is currently rainy, but the rain is expected to stop in 2 hours.
>
> - **Los Angeles (LA):** Rainy, with rain stopping in 2 hours.
> - **New York:** Rainy, with rain stopping in 2 hours.
>
> Let me know if you need further details! 🌦️
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> The agent previously discussed the **weather in Los Angeles (LA) and New York** with the user.
>
> **Tools called:**
>
> 1. `get_weather` with argument `{"location": "LA"}`
> 2. `get_weather` with argument `{"location": "New York"}`
>
> These tool calls retrieved the weather information for both locations.

#### 60 & 61 Streaming Agent Output

###### Streaming in LangGraph

Streaming in LangGraph will only generate streams in `node` level, instead of `token` level

- It will returns a **dictionary** in each node, instead of `Messages`

> {'agent': {'messages': [AIMessage(content='The weather in Los Angeles is currently rainy, but the rain is expected to stop in 2 hours. Similarly, New York is also experiencing rain, with the same forecast of rain stopping in 2 hours. Let me know if you need further details!', additional_kwargs={}, response_metadata={'model': 'qwen3:8b', 'created_at': '2026-xx-xxTxx:xx:xxZ', 'done': True, 'done_reason': 'stop', 'total_duration': 8xx, 'load_duration': 4xx, 'prompt_eval_count': 3xx, 'prompt_eval_duration': 6xx,'eval_count': 1xx, 'eval_duration': 7xx, 'logprobs': None, 'model_name': 'qwen3:8b', 'model_provider': 'ollama'}, id='lc_run--xx', tool_calls=[], invalid_tool_calls=[], usage_metadata={'input_tokens': 3xx, 'output_tokens': 1xx, 'total_tokens': 4xx})]}}

So, it can be printed out as follows:

```
for chunk in agent.stream(initial_state, config=config):
    if "agent" in chunk:
        print(f"[AGENT]: {chunk['agent']['messages'][-1].content}")
    if "tools" in chunk:
        print(f"[TOOLS]: {chunk['tools']['messages'][-1].content}")
```

###### Streaming Result

> [TOOLS]: {"location": "New York", "weather": "rainy, but rain will stop in 2 hours."}
> [AGENT] generating responses...
> [AGENT]: The weather in both Los Angeles and New York is currently **rainy**, with rain expected to stop in **2 hours**.
>
> Let me know if you need further details! 🌧️

####

#### 62. Retrieve Historical Chat Messages

(Skipped)

## Section 8 Short-Term Memory

#### Learning Objectives:

- Understand InMemorySaver vs. SqliteSaver

- Save conversation that survive restarts

- Handle multiple users with thread isolation

#### 63. Production-Ready Memory Architecture

Usually, short-term memory handle `thread ID`, while long-term memory handle `user ID`.

In this section, we will use `sqlite` and `postgreSQL` adaptors.

#### 64. Short-Term vs. Long-Term Memory in Agents

###### Memory

- Short-Term Memory
  - Chat History
  - Checkpointed state
  - Scoped by `thread_id`
- Long-Term Memory
  - Episodic Memory
    - User-specific past interactions, preference
    - Stored externally (DB / vector store)
  - Semantic Memory
    - Knowledge base (LLM weights or RAG corpus)
  - Procedural Memory
    - How to perform tasks
    - Encoded in model weights, prompts, or agent workflow

#### 65. How LLM Updates Chat & Working Memory

In LangGraph

- `State: {"messages": [S1, H1, A1, T1, A2 ...], ...}`
- As query comes in, messages in short-term memory will be loaded (if exists).
- And after the execution, newly generated messages will be attached to the state at the end.

#### 66. Notebook Setup for Persistence

LangGraph: [Checkpointer Libraries](https://docs.langchain.com/oss/python/langgraph/persistence#checkpointer-libraries)

Before starting, necessary libraries should be installed.

```python
uv add langgraph-checkpoint-sqlite
uv add langgraph-checkpoint-postgres
```

In this section, instead of `InMemorySaver`, `SqliteSaver` and `PostgresSaver` will be used here.

- `SqliteSaver` and `PostgresSaver` should be passed in **connection**, instead of DB path.

```python
import sqlite3
from langgraph.checkpoint.sqlite import SqliteSaver

import psycopg
from langgraph.checkpoint.postgres import PostgresSaver
```

#### 67. Store Memories in SQLite

###### Initialize DataBase Connection

```python
db_path = "checkpoint.db"
conn = sqlite3.connect(database=db_path, check_same_thread=False)
checkpointer = SqliteSaver(conn)
```

###### Configure Agent and Chat

```python
def chat(agent, query, thread_id):
    initial_state = AgentState(
        messages=[HumanMessage(query)]
        )

    # Configure thread id
    config = {"configurable" :{"thread_id": thread_id}}

    response = agent.invoke(initial_state, config=config)
    response["messages"][-1].pretty_print()

# Create the agent and chat with it
query = "What is the weather in LA and new york??"
thread_id = "react-agent-building-demo"
agent = create_agent(checkpointer=checkpointer)

chat(agent, query, thread_id)
```

###### Results

Chat history has been stored in `checkpoint.db` in our directory.

Check it using `sqlite3 checkpoint.db`

```
sqlite> .table
checkpoints  writes

sqlite> .schema
CREATE TABLE checkpoints (
                thread_id TEXT NOT NULL,
                checkpoint_ns TEXT NOT NULL DEFAULT '',
                checkpoint_id TEXT NOT NULL,
                parent_checkpoint_id TEXT,
                type TEXT,
                checkpoint BLOB,
                metadata BLOB,
                PRIMARY KEY (thread_id, checkpoint_ns, checkpoint_id)
            );
CREATE TABLE writes (
                thread_id TEXT NOT NULL,
                checkpoint_ns TEXT NOT NULL DEFAULT '',
                checkpoint_id TEXT NOT NULL,
                task_id TEXT NOT NULL,
                idx INTEGER NOT NULL,
                channel TEXT NOT NULL,
                type TEXT,
                value BLOB,
                PRIMARY KEY (thread_id, checkpoint_ns, checkpoint_id, task_id, idx)
            );
```

Our agent will remember the chat history now:

```python
review_query = "What kind of topic does this conversation involve? Please summarize in one or two sentences."
thread_id = "react-agent-building-demo"
agent = create_agent(checkpointer=checkpointer)

chat(agent, review_query, thread_id)
```

```
================================== Ai Message ==================================

This conversation involves checking the current weather conditions for Los Angeles and New York, revealing that both locations are experiencing rain with the same forecast of rain stopping in 2 hours.
```

#### 68. Create Free PostgreSQL DB

(Skipped)

#### 69. Persist Memory to Remote PostgreSQL

```python
# Configure thread id and database path for checkpointing
db_path = "checkpoint.db"
conn = psycopg.connect(conninfo=os.getenv("POSTGRES_CONNINFO"),
                       autocommit=True,
                       prepare_threshold=0)
checkpointer = PostgresSaver(conn)

# This is to initiate tables
checkpointer.setup()
```

#### 70. Alternative Ways to Connect to PostgreSQL

```python
with PostgresSaver.from_conn_string(os.getenv("POSTGRES_CONNINFO")) as checkpointer:
    agent = create_agent(checkpointer=checkpointer)
    review_query = "How many times I have asked you? What queries did I ask?"
    thread_id = "react-agent-building-demo"
    chat(agent, review_query, thread_id)
```

We can see that our agent answered questions precisely.

> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> 1. "What kind of topic does this conversation involve? Please summarize in one or two sentences."
> 2. "How many times I have asked you? What queries did I ask?"
>
> You have asked **2 times** in total. Let me know if you need further clarification!

## Section 9: Long-Term Memory

In this section, we will focus on `user ID` and `long-term` memory.

- Note that `Saver` is for short-term memory, while `Store` is for long-term memory.
- `user ID` is not directly used, instead, `namespace` should be used as a **tuple**
  - User ID
    - Preference - namespace
      - food
      - taste
    - Address - namespace
      - city
      - street
      - room number

#### 71. Intro to Long-Term Memory

`Vector search` will be used to search and match user memory.

In this lesson, we will use Postgres

```python
from langgraph.store.sqlite import SqliteStore
from langgraph.store.postgres import PostgresStore
```

#### 72. PostgreSQL Setup for Short-Term + Long-Term Memory

`Ollama Embedding Models` will be used to convert strings to vectors.

The dimension is 768 in `nomic-embed-text`: [HuggingFace](https://huggingface.co/nomic-ai/nomic-embed-text-v1.5#adjusting-dimensionality)

```python
from langchain_ollama import OllamaEmbeddings

EMBEDDING_MODEL = "nomic-embed-text"
```

###### Sample Code

```python
# =============================================
# Store and Saver Setup
# =============================================
def setup_memory(postgres_conninfo: str):
    # Short term memory saver using Postgres, for checkpointing the agent state and conversation history
    checkpointer_conn = psycopg.connect(conninfo=postgres_conninfo, autocommit=True, prepare_threshold=0)
    checkpointer = PostgresSaver(checkpointer_conn)
    checkpointer.setup()     # first time setup the database tables for the store

    # Long term memory store and saver using Postgres
    store_conn = psycopg.connect(conninfo=postgres_conninfo, autocommit=True, prepare_threshold=0)
    store = PostgresStore(store_conn, index={'embed': embed_texts, 'dims': 768})
    store.setup()           # first time setup the database tables for the store

    return checkpointer, store

checkpointer, store = setup_memory(POSTGRES_CONNINFO)
```

#### 73 ~ 75. Long-Term Memory Tools - store

###### Memory Operations

Memory in LangGraph basically adapts a `key-value` pair to store data.

- `put`
- `get`
- `search`
- `delete`

###### Memory in Action

```python
# =============================================
# Store and Retrieve Memories
# =============================================
user_id = "test_user_123"
namespace = (user_id, "preferences")

# Save some user preferences in the store
# store.put(namespace=namespace, key="food", value={"favorite": ["pizza", "pasta"], "least_favorite": "broccoli"})
# store.put(namespace=namespace, key="color", value={"favorite": ["blue", "green"], "least_favorite": "yellow"})

# Retrieve user preferences from the store - get by key
user_food_preference = store.get(namespace=namespace, key="food")
print(f"User food preference: {user_food_preference}")

# Retrieve user color preference from the store - get by semantic search
query = "What is the user's favorite color?"
retrieved_items = store.search(namespace, query=query, limit=1)
print(f"Retrieved items for query '{query}':\n{retrieved_items}")

# Delete a key from the store
# store.delete(namespace=namespace, key="color")
```

###### Results

- `get` method only extract value by using a specific key
  - Return a single `Item`
- `search` method will match user's query using embedded vectors and find the most close match (limit=1)
  - Return a list of `Item`

> User food preference: Item(namespace=['test_user_123', 'preferences'], key='food', value={'favorite': ['pizza', 'pasta'], 'least_favorite': 'broccoli'}, created_at='2026-xx-xxTxx:xx:xx.xx+xx:00', updated_at='xx')
>
> Retrieved items for query 'What is the user's favorite color?':
> [Item(namespace=['test_user_123', 'preferences'], key='color', value={'favorite': ['blue', 'green'], 'least_favorite': 'yellow'}, created_at='2026-xx-xxTxx:xx:xx.xx+xx:00', updated_at='xx', score=0.78xxx)]

#### 76 & 77. Create Memory Management Tools

`get_user_memory` and `save_user_memory` are created to manage user's long-term memory

- `search` can also be applied here to search for preferences.

```python
# =============================================
# Tools for Memory Management
# =============================================
@tool
def get_user_memory(user_id: str, category: str) -> dict:
    """
    Retrieve user preference or information from long term memory

    Args:
        user_id: User identifier
        category: Category of information (e.g. 'food', 'hobbies', 'schedule', 'location)
    """
    namespace = (user_id, "preference")

    try:
        item = store.get(namespace=namespace, key=category)
        return {"status": "succeeded",
                "error": "N/A",
                "data_retrieved": item.value}
    except Exception as e:
        return {"status": "failed",
                "error": e,
                "data_retrieved": "Not Found"}

@tool
def save_user_memory(user_id: str, category: str, information: dict) -> dict:
    """
    Save user preference or information to long-term memory.

    Args:
        user_id: User identifier
        category: Category of information (e.g. 'food', 'hobbies', 'schedule', 'location)
        information: Dictionary that containing the information to use
    """
    namespace = (user_id, "preferrence")
    try:
        store.put(namespace=namespace, key=category, value=information)
    except Exception as e:
        return {"status": "failed",
                "error": e}
    return {"status": "succeeded", "error": "N/A"}
```

#### 78 ~ 80. Create Agent Node with Memory Tools

```python
def agent_node(state: AgentState):
    # Bind tools to the LLM, so that it can call tools during generation.
    llm_with_tools = llm.bind_tools(tools=TOOLS)

    user_id = state.get("user_id", "unknown")
    namespace = (user_id, "preference")

    last_message = state["messages"][-1].content
    memories = store.search(namespace, query=last_message, limit=3)

    # build context memory for personalized answer
    context_line = []
    for mem in memories:
        text = f" - {mem.key}: {mem.value}"
        context_line.append(text)
    memory_text = "\n\n".join(context_line) if context_line else "No user preference found in the store yet."
    print(f"User memory retrieved: {memory_text}")

    SYSTEM_PROMPT = f"""
                    You are a helpful assistant with long-term memory capabilities and access to utility tools.

                        User ID: {user_id}
                        Current User Memories:
                        {memory_text}

                        MEMORY TOOLS USAGE:

                        1. save_user_memory: Use when user shares NEW information
                        - Always pass user_id: "{user_id}"
                        - Food preferences (diet, likes, dislikes, allergies)
                        - Work information (role, company, interests)
                        - Hobbies and activities
                        - Schedule and availability
                        - Location and timezone

                        2. get_user_memory: Use when you need to recall specific category
                        - Always pass user_id: "{user_id}"
                        - When answering questions about past preferences
                        - When user asks "what do you know about me?"
                        - When making recommendations based on preferences

                        UTILITY TOOLS USAGE:
                        3. get_weather: Use to retrieve current weather information
                        - Pass location as parameter (city name, zip code, or coordinates)
                        - Use when user asks about weather conditions
                        - Use when planning activities that depend on weather
                        - Examples: "What's the weather in London?", "Will it rain today?"

                        4. calculate: Use to perform mathematical calculations
                        - Pass mathematical expression as string parameter
                        - Supports basic arithmetic (+, -, *, /)
                        - Supports advanced operations (powers, roots, trigonometry)
                        - Use when user needs numerical computations
                        - Examples: "What's 15% of 250?", "Calculate the area of a circle with radius 5"

                        GUIDELINES:
                        - Always save when user shares personal information
                        - Retrieve specific categories when needed for context
                        - Use semantic search results shown above for general context
                        - Use get_weather when location-based weather info is needed
                        - Use calculate for any mathematical operations or conversions
                        - Be conversational and natural when using all tools
                        - Combine tools when appropriate (e.g., weather + saved location preference)
                    """

    system_message = SystemMessage(SYSTEM_PROMPT)
    messages = [system_message] + state["messages"]
    response = llm_with_tools.invoke(messages)

    # AIMessages will contain tool_calls attributes during tool call turn
    if hasattr(response, "tool_calls") and response.tool_calls:
        for tc in response.tool_calls:
            print(f"This agent called tool: {tc.get('name', '?')} with args: {tc.get('args', '?')}")
    else:
        print(f"[AGENT] generating responses...")

    # The value of messages should be list, because of operator.add
    return {"messages": [response]}
```

#### 81. Create LangGraph Agent

```python
# Build the agent graph
def create_agent(checkpointer):
    # Get graph canvas
    # The canvas should accept state schema, instead of state instance
    builder = StateGraph(state_schema=AgentState)

    builder.add_node("agent", agent_node)
    builder.add_node("tools", ToolNode(tools=TOOLS)) # Should be the same with that in routing

    builder.add_edge(START, "agent")
    builder.add_conditional_edges(source="agent", path=should_continue, path_map=["tools", END])
    builder.add_edge("tools", "agent")  # Do not forget to connect tool node back to agent

    graph = builder.compile(checkpointer=checkpointer)

    return graph
```

#### 82. Take Fresh Store and Saver Connection in Agent Node

`user_id` for long-term memory, and `thread_id` for short-term memory.

- `user_id` is used to extract user's information by `store.get` or `store.search`
- `thread_id` is used to configure checkpointer

```python
# Define chat function to interact with the agent
def chat(agent, query, user_id, thread_id):
    initial_state = AgentState(
        messages=[HumanMessage(query)],
        user_id=user_id
        )

    # Configure thread id
    config = {"configurable" :{"thread_id": thread_id}}

    response = agent.invoke(initial_state, config=config)
    response["messages"][-1].pretty_print()
```

#### 83. Agent with Long-term and Short-term Memory in Action

> Enter your query (or '/exit' to quit): tell me the weather in the city I currently live.
> User memory retrieved: No user preference found in the store yet.
> This agent called tool: get_user_memory with args: {'user_id': 'demo-user-001', 'category': 'location'}
> User memory retrieved: No user preference found in the store yet.
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> I don't have access to your current location information. Could you please tell me which city you're currently living in? Once you share that, I can check the weather for you.
>
> Enter your query (or '/exit' to quit): I live in LA, and I prefer to eat strawberry and watermelon.
> User memory retrieved: No user preference found in the store yet.
> This agent called tool: save_user_memory with args: {'user_id': 'demo-user-001', 'category': 'location', 'information': {'city': 'LA'}}
> This agent called tool: save_user_memory with args: {'user_id': 'demo-user-001', 'category': 'food', 'information': {'preferences': ['strawberry', 'watermelon']}}
> User memory retrieved: No user preference found in the store yet.
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> The weather in Los Angeles is currently 72°F with clear skies. It looks like a perfect day to enjoy your favorite fruits—strawberry and watermelon! 🍓🍉 Let me know if you need further details.

> Enter your query (or '/exit' to quit): cool, I would like to take a tour at London next week, tell me if there is my favourate food there.
> User memory retrieved: No user preference found in the store yet.
> This agent called tool: get_weather with args: {'location': 'London'}
> User memory retrieved: No user preference found in the store yet.
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> The weather in London is currently rainy, but the rain is expected to stop in 2 hours. 🌧️ While you wait for the rain to clear, here are some food recommendations in London:
>
> 1. **Street Food**: Try fresh strawberries (a local favorite!) or watermelon at markets like Camden or Borough Market.
> 2. **Indoor Options**: If the rain lingers, enjoy a cozy meal at a traditional British pub or try a seafood dish at a riverside restaurant.
> 3. **Fruit Markets**: London’s markets often have seasonal fruits, including strawberries in summer.
>
> Let me know if you’d like help planning a specific activity or meal!

## Section 10: Guardrail, Interrupt and Human in the Loop

So far, we have worked with agent that is completely autonomous, however, it is may not be a good idea.

There are some components in your system that you would like to only execute it under your approval.

For example, money transfer, deleting files, etc.

#### 84. Introduction to Human in the Loop and PII Guardrail

`PII` refers to **personal identification**. However, unlike langchain, there is no prebuilt PII Guardrail here in LangGraph, because it is highly customizable.

`Human In the Loop` occurs in `tool calling`, it stops the tools from executing and end the loop, until the approval is given.

###### Interrupt and Command

LangGraph: [Interrupts](https://docs.langchain.com/oss/python/langgraph/interrupts)

Interrupts allow you to pause graph execution at specific points and wait for external input before continuing.

This enables human-in-the-loop patterns where you need external input to proceed.

- to use `interrupt`, you need a **checkpointer** and a **thread_id**
- when `interrupt` is called, graph execution is suspended, state is saved and a special value `__interrupt` is returned.
- Using `Command(resume=...)` to continue, you must have the same `thread_id`

#### 85. HITL Notebook Setup

(skipped)

#### 86. Create Transfer Money Tool with Interrupt for User Approval

```python
# =============================================
# Transfer Money Tool
# =============================================
@tool
def transfer_money(amount: int, recipient: str) -> dict:
    """
    Transfer moneny. Large transfers require approval

    Args:
        amount (int): Amount to transfer in dollars
        recipient (str): Recipient of the transfer
    """
    if amount > 1000:
        approval = interrupt(
            {
                "type": "approval_required",
                "amount": amount,
                "recipient": recipient
            }
        )
        if approval.get("decision") != "approve":
            return {"status": "canceled", "amount": amount, "recipient": recipient}

    return {"status": "success", "amount": amount, "recipient": recipient}
```

#### 87. Create PII Guardrail Node

###### Pattern Recognition

Regex 101: [Regular Expressions 101](https://regex101.com/)

There are some ready-to-use sample of regular expression for identification of certain types in Regex 101.

```python
# =============================================================================
# Guardrail Node - PII Detection
# =============================================================================
# PII Pattern Definitions
patterns = {
        "SSN": r'\b\d{3}-\d{2}-\d{4}\b',  # SSN: 123-45-6789
        "Credit Card": r'\b\d{4}[\s-]?\d{4}[\s-]?\d{4}[\s-]?\d{4}\b',  # Credit Card: 1234-5678-9012-3456
        "Mobile Number": r'\b(\+?\d{1,3}[-.\s]?)?\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}\b',  # Mobile: +1-234-567-8900
        "Email": r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b',  # Email: user@example.com
        "URL/Link": r'https?://[^\s]+|www\.[^\s]+'  # URL: http://example.com or www.example.com
    }
```

###### Guardrail Node

Here, we define a guardrail node which use `re.match` to examine if user's input matches some of the patterns above.

- If matching, a conditional edge will connect this node to END node. The phrases in `SystemMessage` will be presented to user
- User's query will flow to agent node if no matches.

```python
def guardrail_node(state: AgentState):
    last_message = state["messages"][-1].content

    for pii_type, pii_pattern in patterns.items():
        if re.search(pattern=pii_pattern, string=last_message):
            # Will be connected to the END node and share with user
            return {
                "messages": [SystemMessage(content=f"Request Blocked: Contains {pii_type}.\nPlease Do not share sensitive personal information to the agent")]
            }
```

#### 88. Create Agent Node

(skipped)

#### 89. Create Agent and Guardrail Router Conditional Edges

(Skipped)

#### 90. Create SQLite Saver for Agent State Persistence

(Skipped)

#### 91. Create Agent with PII Guardrail Protection

(Skipped)

#### 92. Execute Agent with PII Guardrail and Money Transfer Tool

```python
query = "Write an email to Alice. Her email address is example@email.com"
response = agent.invoke(input= AgentState(messages=[HumanMessage(query)],user_id="PII-user-001"),
                        config={"configurable" :{"thread_id": "agent-PII-demo-1"}})
response["messages"][-1].pretty_print()
```

> PII detected. Type Email
> ================================ System Message ================================
>
> Request Blocked: Contains Email.
> Please Do not share sensitive personal information to the agent

#### 93. Execute Agent with Human In the Loop Approval

###### Interrupt

```python
query = "Please transfer $1500 to Alice."
response = agent.invoke(input= AgentState(messages=[HumanMessage(query)],user_id="HITL-user-004"),
                        config={"configurable" :{"thread_id": "agent-HITL-demo-4"}})
print(response)
```

In the responses below, we can see that:

- When `transfer_money` is called, and the amount is larger than $1000, the graph is stoped and returns a state
- In the state, a key-value pair called `__interrupt__` is returned
  - `type` is exactly what we defined in `interrupt` function

```json
{
  "user_id": "HITL-user-004",
  "is_sensitive": False,
  "messages": [
    {
      "type": "HumanMessage",
      "content": "Please transfer $1500 to Alice."
    },
    {
      "type": "AIMessage",
      "content": "",
      "tool_calls": [
        {
          "name": "transfer_money",
          "args": {
            "amount": 1500,
            "recipient": "Alice"
          },
          "id": "1fxx"
        }
 ...
    }
  ],
  '__interrupt__':
  [Interrupt(value={'type': 'approval_required',
                    'amount': 1500,
                    'recipient': 'Alice'},
             id='ed897773d917c5b4834683a6f872dead')]}
}
```

###### Resume

Then we can resume our tool calling using `Command`.

```python
response = agent.invoke(input= Command(resume={"decision": "approve"}),
                        config={"configurable" :{"thread_id": "agent-HITL-demo-4"}})
```

`__interrupt__` key-value pair disappeared in our `AgentState`, a normal `AIMessage` is generated in messages.

> AIMessage(content='The transfer of $1500 to Alice has been successfully processed. Let me know if you need further assistance!',...)

#### 94. Stress Test of Agent with PII Guardrail and HITL Approval Workflow

(Skipped)

#### Sample Code:

###### Architecture

```
                                  +-------------+
                                  |  __start__  |
                                  +-------------+
                                        |
                                        v
                                +----------------+
                                | PII Guardrail 	| -------
                                +----------------+				|
                                        |									|
                                        v									|
                                +----------------+				|
                                |    LLM/Agent   |				|
                                +----------------+				|
                                 |    |       |						|
                        (call tool)   |   	(finish)			|
                                 |    |       |						|
                                 v    |       v						|
                           +------------+     |						|
                           |    Tool    |     |						|
                           +------------+     |						|
                                              |						|
                                              |						|
                                              v						v
                                             +-------------+
                                             |   __end__   |
                                             +-------------+
```

###### Code

```python
import os
import re
import operator
import requests
from dotenv import load_dotenv
from typing import TypedDict, Annotated

from langchain_ollama import ChatOllama, OllamaEmbeddings
from langgraph.graph import StateGraph, START, END
from langgraph.prebuilt import ToolNode
from langchain_core.tools import tool
from langchain_core.messages import SystemMessage, AIMessage, HumanMessage

from langgraph.types import Command, interrupt

# Use Postgres
import psycopg
from langgraph.checkpoint.postgres import PostgresSaver
from langgraph.store.postgres import PostgresStore


# =============================================
# Configuration
# =============================================

# Load environment variables from .env file, so that LangSmith tracing is enabled.
load_dotenv()

# Configuration for Ollama server and model
BASE_URL = "http://localhost:11434"
MODEL_NAME = "qwen3:8b"
EMBEDDING_MODEL = "nomic-embed-text"
POSTGRES_CONNINFO = os.getenv("POSTGRES_CONNINFO")

# Initialize the LLM and embeddings
llm = ChatOllama(model=MODEL_NAME, base_url=BASE_URL)
embeddings = OllamaEmbeddings(model=EMBEDDING_MODEL, base_url=BASE_URL)

# Define the state schema for the agent. The state will keep track of the conversation messages.
class AgentState(TypedDict):
    messages: Annotated[list, operator.add]
    user_id: str
    is_sensitive: bool  # flag to indicate if the last message contains sensitive information


# =============================================
# Store and Saver Setup
# =============================================
# Define a simple embedding function
def embed_texts(texts: list[str]) -> list[list[float]]:
    return embeddings.embed_documents(texts)

# Set up memory saver and store
def setup_memory(postgres_conninfo: str):
    # Short term memory saver using Postgres, for checkpointing the agent state and conversation history
    checkpointer_conn = psycopg.connect(conninfo=postgres_conninfo, autocommit=True, prepare_threshold=0)
    checkpointer = PostgresSaver(checkpointer_conn)
    checkpointer.setup()     # first time setup the database tables for the store

    # Long term memory store and saver using Postgres
    store_conn = psycopg.connect(conninfo=postgres_conninfo, autocommit=True, prepare_threshold=0)
    store = PostgresStore(store_conn, index={'embed': embed_texts, 'dims': 768}) # embedding dimension is 768 for nomic-embed-text
    store.setup()           # first time setup the database tables for the store

    return checkpointer, store

checkpointer, store = setup_memory(POSTGRES_CONNINFO)

# =============================================
# Transfer Money Tool
# =============================================
@tool
def transfer_money(amount: int, recipient: str) -> dict:
    """
    Transfer moneny. Large transfers require approval

    Args:
        amount (int): Amount to transfer in dollars
        recipient (str): Recipient of the transfer
    """
    if amount > 1000:
        approval = interrupt(
            {
                "type": "approval_required",
                "amount": amount,
                "recipient": recipient
            }
        )
        if approval.get("decision") != "approve":
            return {"status": "canceled", "amount": amount, "recipient": recipient}

    return {"status": "success", "amount": amount, "recipient": recipient}

# =============================================
# Tools for Memory Management
# =============================================

@tool
def get_user_memory(user_id: str, category: str) -> dict:
    """
    Retrieve user preference or information from long term memory

    Args:
        user_id: User identifier
        category: Category of information (e.g. 'food', 'hobbies', 'schedule', 'location)
    """
    namespace = (user_id, "preference")

    try:
        item = store.get(namespace=namespace, key=category)
        return {"status": "succeeded",
                "error": "N/A",
                "data_retrieved": item.value}
    except Exception as e:
        return {"status": "failed",
                "error": e,
                "data_retrieved": "Not Found"}


@tool
def save_user_memory(user_id: str, category: str, information: dict) -> dict:
    """
    Save user preference or information to long-term memory.

    Args:
        user_id: User identifier
        category: Category of information (e.g. 'food', 'hobbies', 'schedule', 'location)
        information: Dictionary that containing the information to use
    """
    namespace = (user_id, "preferrence")
    try:
        store.put(namespace=namespace, key=category, value=information)
    except Exception as e:
        return {"status": "failed",
                "error": e}
    return {"status": "succeeded", "error": "N/A"}


# =============================================
# General Tools
# =============================================

# Define a tool for getting weather information.
@tool
def get_weather(location: str) -> dict:
    """Get current weather for a location.

    Use for queries about weather, temperature, or conditions in any city.
    Examples: "weather in Paris", "temperature in Tokyo", "is it raining in London"

    Args:
        location: City name (e.g., "New York", "London", "Tokyo")

    Returns:
        Current weather information including temperature and conditions.
    """

    # In a real implementation, you would call an actual weather API here.
    # url = f"https://wttr.in/{location}?format=j1"
    # response = requests.get(url=url, timeout=10)
    # response.raise_for_status()
    # data = response.json()

    # hard-coding because wttr.in is down
    weather_data = {
        "location": location,
        "weather": "rainy, but rain will stop in 2 hours."}

    return weather_data

# Define the list of tools that the agent can use. This will be passed to the ToolNode in the graph.
TOOLS = [get_user_memory, save_user_memory, get_weather, transfer_money]


# =============================================
# Guardrail Node for PII Detection
# =============================================

# PII Pattern Definitions
patterns = {
        "SSN": r'\b\d{3}-\d{2}-\d{4}\b',  # SSN: 123-45-6789
        "Credit Card": r'\b\d{4}[\s-]?\d{4}[\s-]?\d{4}[\s-]?\d{4}\b',  # Credit Card: 1234-5678-9012-3456
        "Mobile Number": r'\b(\+?\d{1,3}[-.\s]?)?\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}\b',  # Mobile: +1-234-567-8900
        "Email": r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b',  # Email: user@example.com
        "URL/Link": r'https?://[^\s]+|www\.[^\s]+'  # URL: http://example.com or www.example.com
    }

def guardrail_node(state: AgentState):
    last_message = state["messages"][-1].content

    for pii_type, pii_pattern in patterns.items():
        if re.search(pattern=pii_pattern, string=last_message):
            print(f"PII detected. Type {pii_type}")
            # Will be connected to the END node and share with user
            return {
                "messages": [AIMessage(content=f"Request Blocked: Contains {pii_type}.\nPlease Do not share sensitive personal information to the agent")],
                "is_sensitive": True
            }
    else:
        return {
            "is_sensitive": False,
        }


# =============================================
# Agent Node with Long-Term and Short-Term Memory
# =============================================
def agent_node(state: AgentState):
    # Bind tools to the LLM, so that it can call tools during generation.
    llm_with_tools = llm.bind_tools(tools=TOOLS)

    user_id = state.get("user_id", "unknown")
    namespace = (user_id, "preference")

    last_message = state["messages"][-1].content
    memories = store.search(namespace, query=last_message, limit=3)

    # build context memory for personalized answer
    context_line = []
    for mem in memories:
        text = f" - {mem.key}: {mem.value}"
        context_line.append(text)
    memory_text = "\n\n".join(context_line) if context_line else "No user preference found in the store yet."

    SYSTEM_PROMPT = f"""
                    You are a helpful assistant with long-term memory capabilities and access to utility tools.

                        User ID: {user_id}
                        Current User Memories:
                        {memory_text}

                        MEMORY TOOLS USAGE:

                        1. save_user_memory: Use when user shares NEW information
                        - Always pass user_id: "{user_id}"
                        - Food preferences (diet, likes, dislikes, allergies)
                        - Work information (role, company, interests)
                        - Hobbies and activities
                        - Schedule and availability
                        - Location and timezone

                        2. get_user_memory: Use when you need to recall specific category
                        - Always pass user_id: "{user_id}"
                        - When answering questions about past preferences
                        - When user asks "what do you know about me?"
                        - When making recommendations based on preferences

                        UTILITY TOOLS USAGE:
                        3. get_weather: Use to retrieve current weather information
                        - Pass location as parameter (city name, zip code, or coordinates)
                        - Use when user asks about weather conditions
                        - Use when planning activities that depend on weather
                        - Examples: "What's the weather in London?", "Will it rain today?"

                        4. transfer_money: Use to transfer money. Large transfers over $1000 require approval.
                        - Pass amount and recipient as parameters
                        - Use when user asks to transfer money
                        - Examples: "Send $1500 to Bob"

                        GUIDELINES:
                        - Always save when user shares personal information
                        - Retrieve specific categories when needed for context
                        - Use semantic search results shown above for general context
                        - Use get_weather when location-based weather info is needed
                        - Use calculate for any mathematical operations or conversions
                        - Be conversational and natural when using all tools
                        - Combine tools when appropriate (e.g., weather + saved location preference)
                    """

    system_message = SystemMessage(SYSTEM_PROMPT)
    messages = [system_message] + state["messages"]
    response = llm_with_tools.invoke(messages)

    # AIMessages will contain tool_calls attributes during tool call turn
    if hasattr(response, "tool_calls") and response.tool_calls:
        for tc in response.tool_calls:
            print(f"This agent called tool: {tc.get('name', '?')} with args: {tc.get('args', '?')}")
    else:
        print(f"[AGENT] generating responses...")

    # The value of messages should be list, because of operator.add
    return {"messages": [response]}

# =============================================
# Conditional Edge
# =============================================

# Guardrail, agent
def guardrail_router(state: AgentState):
    is_sensitive = state["is_sensitive"]

    if is_sensitive:
        return END
    else:
        return "agent"

# Define the routing function
def should_continue(state:AgentState):
    last_message = state["messages"][-1]

    if hasattr(last_message, "tool_calls") and last_message.tool_calls:
        return "tools"      # This key should be the same with tool node
    else:
        return END

# =============================================
# Graph
# =============================================

# Build the agent graph
def create_agent(checkpointer):
    # Get graph canvas
    # The canvas should accept state schema, instead of state instance
    builder = StateGraph(state_schema=AgentState)

    builder.add_node("guardrail", guardrail_node)
    builder.add_node("agent", agent_node)
    builder.add_node("tools", ToolNode(tools=TOOLS)) # Should be the same with that in routing

    builder.add_edge(START, "guardrail")
    builder.add_conditional_edges(source="guardrail", path=guardrail_router, path_map=["agent", END])
    builder.add_conditional_edges(source="agent", path=should_continue, path_map=["tools", END])
    builder.add_edge("tools", "agent")  # Do not forget to connect tool node back to agent

    graph = builder.compile(checkpointer=checkpointer)

    return graph

# Define chat function to interact with the agent
def chat(agent, query, user_id, thread_id) -> AgentState:
    initial_state = AgentState(
        messages=[HumanMessage(query)],
        user_id=user_id
        )

    # Configure thread id
    config = {"configurable" :{"thread_id": thread_id}}

    response = agent.invoke(initial_state, config=config)
    return response


# =============================================
# Main Loop for Chatting with the Agent
# =============================================

# Create the agent and chat with it
user_id = "demo-user-001"
thread_id = "agent-with-memory-HITL-001"
agent = create_agent(checkpointer=checkpointer)


# main loop for chatting with the agent
if __name__ == "__main__":
    while True:
        query = input("Enter your query (or '/exit' to quit): ")
        if query.lower() == "/exit":
            break
        response = chat(agent, query, user_id, thread_id)
        if "__interrupt__" in response:
            approval_info = response["__interrupt__"][0].value
            print(f"Approval required: You are sending {approval_info.get('amount', 'unknown')} to {approval_info.get('recipient', 'unknown')}.")
            approval = input("Do you approve this move (enter 'approve' or 'disapprove'): ")
            execution = agent.invoke(input=Command(resume={"decision": approval}), config={"configurable" :{"thread_id": thread_id}})
            execution["messages"][-1].pretty_print()
        else:
            response["messages"][-1].pretty_print()
```

###### Tests

4 rounds of tests are executed below:

- PII Test, sensitive infos like `example@email.com` is detected
- Small money transfer: no approval is needed before money transfer
- Larger money transfer: approval is asked, and transfer is executed after getting approval
- Summary (Memory Test): the agent successfully summarizes the money transfers so far.

Round 1:

> Enter your query (or '/exit' to quit): Transfer 500 to example@email.com
> PII detected. Type Email
> ================================ System Message ================================
>
> Request Blocked: Contains Email.
> Please Do not share sensitive personal information to the agent

Round 2:

> Enter your query (or '/exit' to quit): Can you transfer 100 to Alice
> User memory retrieved: No user preference found in the store yet.
> This agent called tool: transfer_money with args: {'amount': 100, 'recipient': 'Alice'}
> User memory retrieved: No user preference found in the store yet.
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> Transfer of $100 to Alice was successful. Let me know if you need anything else!

Round 3:

> Enter your query (or '/exit' to quit): Give Bob 1500 by bank transfer.
> User memory retrieved: No user preference found in the store yet.
> This agent called tool: transfer_money with args: {'amount': 1500, 'recipient': 'Bob'}
> Approval required: {'type': 'approval_required', 'amount': 1500, 'recipient': 'Bob'}
> Do you approve this move (enter 'approve' or 'disapprove'): approve
> User memory retrieved: No user preference found in the store yet.
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> Transfer of $1500 to Bob was successful. Let me know if you need anything else!

Round 4:

> Enter your query (or '/exit' to quit): Hi, can you summarize the money transfer you have done so far?
> User memory retrieved: No user preference found in the store yet.
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> Here's a summary of the transfers I've processed for you:
>
> 1. **$100** transferred to Alice
> 2. **$1500** transferred to Bob
>
> Total amount transferred: **$1600**.  
> Let me know if you need further assistance! 😊
> Enter your query (or '/exit' to quit): /exit

## Section 11: Reflection Agent

#### 95. Introduction to Reflection Agent

LangChain Blog: [Reflection Agents](https://blog.langchain.com/reflection-agents/)

AutoGen: [Reflection](https://microsoft.github.io/autogen/stable//user-guide/core-user-guide/design-patterns/reflection.html)

Previously,

`Researcher` and `critic` agents are introduced in `reflection agent`

- Research agent has tools to act/get information
  - Answer generated by research agent will be evaluated by critic agent
- Critic agent can give a feedback to researcher agent
  - Only critic agent can end the execution and response to user

###### Architecture

                                  +-------------+
                                  |  __start__  |
                                  +-------------+
                                        |
                                        v
                                +----------------+
                                |    Researcher	 |
                                |				Agent    |--------
                                +----------------+				|
                                 |    |       	|					|
                        (call tool)   |   			|			 		|
                                 |    |       	|					|
                                 v    |       	|					|
                           +------------+     	|					|
                           |    Tool    |     	|					|
                           +------------+     	|					|
                                              	|					|
    																						v 				|
                                            +----------------+
                                            |  Critic Agent  |
                                            +----------------+
                                                    |
                                                    v
                                             +-------------+
                                             |   __end__   |
                                             +-------------+

#### 96. Introduction to Free Web Search Tool - DDGS

###### Web Search Tool

DDGS: [GitHub HomePage](https://github.com/deedy5/ddgs?tab=readme-ov-file)

Tavily search, Dev Serper and DDGS (Duck Duck Go) are choices for you.

We will use `text()` method of `DDGS` class to search for information online.

- need query and max try times as input
- return lists of dictionary of search results

```bash
uv add ddgs
```

#### 97. Create and Test Free Web Search Tool for Reflection Agent

```python
@tool
def web_search(query: str, num_results:int = 10, region:str = "us-en") -> dict:
    """
    Use this tool whenever you need to access real time or latest information.
    Search the web using DuckDuckGo

    Args:
        query: search query string.
        num_results: Number of results to return (default: 5)
        region: region code for localized search results (default: "us-en")

    Returns:
        Formatted search results with titles, descriptions and URLs
    """
    ddgs = DDGS()
    results = []

    print("Performing web search with query:", query)

    for r in ddgs.text(query, max_results=num_results, region=region):
        results.append({
            "title": r.get("title"),
            "description": r.get("body"),
            "url": r.get("href")
        })
    print(f"Web search completed. Found {len(results) if results else 0} results.")

    if not results:
        results.append({
            "title": "No results found",
            "description": f"No search results were found for the query: {query}",
            "url": ""
        })

    return results
```

#### 98. Create Researcher Agent with Critique Feedback Prompt

###### Agent State

Three more fields are added to state:

- `research` to record the results generated by researcher agent
- `critique` to record the feedback from critic agent in current round
  - Will be send to research agent for reference and next generation
- `iteration` to track the number of rounds, to avoid endless loop

```python
class AgentState(TypedDict):
    messages: Annotated[list[SystemMessage | HumanMessage], operator.add]
    research: str
    critique: str
    iteration: int # To track the number of iterations for reflection
```

###### Researcher Agent

Note that only researcher agent can have access to tools. Critic agent only provide feedbacks.

#### 99. Create Critique Agent Node to Evaluate Researcher Agent Answer

#### 100. Create Researcher and Critique Agents Routing Logic

#### 101. Create Reflection Agent

#### 102. Evaluate and Test Reflection Agent

## Section 13: Build LangGraph Agent with Airbnb MCP Servers

Anthropic: [Introducing the Model Context Protocol](https://www.anthropic.com/news/model-context-protocol)

MCP: [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro)

MCP Servers: [GitHub Pages](https://github.com/modelcontextprotocol/servers)

Airbnb MCP Server: [HomePage](https://github.com/openbnb-org/mcp-server-airbnb)

MCP (Model Context Protocol) is an open-source standard for connecting AI applications to external systems.

#### 118. Introduction to MCP

MCP is introduced by Anthropic on 25th November 2024.

We use MCP to enable our agent to connect with the tools and resources.

MCP contains:

- MCP Host
  - Claude Desktop, IDE, or AI Framework
- MCP Client
  -
- MCP Server
  - Remote or Local
  - `stdio` or `sse/streamable http`
  - Tools, Resources and Prompts

#### 119. Install Node.js for MCP and LangChain MCP Adapter

###### Basic Setups

`node.js` here is required to use Airbnb's MCP server.

```bash
node --version
# v25.2.1
```

#### 120. Connect LangChain MCP Client with Airbnb MCP Server

LangChain Docs: [Model Context Protocol (MCP)](https://docs.langchain.com/oss/python/langchain/mcp)

LangChain MCP Adapters: [GitHub](https://github.com/langchain-ai/langchain-mcp-adapters)

###### Library Installation

```bash
uv add langchain-mcp-adapters
```

- Establish connection to MCP server using `MultiServerClient`
- Acquire a full list of tools using `client.list_tools`

```python
from langchain_mcp_adapters.client import MultiServerMCPClient
import asyncio

async def get_tools():
    mcp_client = MultiServerMCPClient(
        connections={
            "airbnb": {
                "command": "npx",
                "args": [
                    "-y",
                    "@openbnb/mcp-server-airbnb"
                    ],
                "transport": "stdio"
                },
        }
    )

    tools = await mcp_client.get_tools()
    print(f"{len(tools)} tools loaded from Airbnb MCP servers.")
    print(f"Loaded tools: {tools}")
    return tools
```

> [2026-03-05] [INFO] Airbnb MCP Server starting: {
> "version": "0.1.3",
> "ignoreRobotsTxt": false,
> "nodeVersion": "v25.2.1",
> "platform": "darwin"
> }
> [2026-03-05] [INFO] Fetching robots.txt from Airbnb
> [2026-03-05] [INFO] Successfully fetched robots.txt
> [2026-03-05] [INFO] Airbnb MCP Server running on stdio: {
> "version": "0.1.3",
> "robotsRespected": true
> }
> 2 tools loaded from Airbnb MCP servers.
> Loaded tools:
>
> [StructuredTool(name='airbnb_search', description='Search for Airbnb listings with various filters and pagination. Provide direct links to the user', args_schema={'type': 'object', 'properties': {'location': {'type': 'string', 'description': 'Location to search for (city, state, etc.)'}, 'placeId': {'type': 'string', 'description': 'Google Maps Place ID (overrides the location parameter)'}, 'checkin': {'type': 'string', 'description': 'Check-in date (YYYY-MM-DD)'}, 'checkout': {'type': 'string', 'description': 'Check-out date (YYYY-MM-DD)'}, 'adults': {'type': 'number', 'description': 'Number of adults'}, 'children': {'type': 'number', 'description': 'Number of children'}, 'infants': {'type': 'number', 'description': 'Number of infants'}, 'pets': {'type': 'number', 'description': 'Number of pets'}, 'minPrice': {'type': 'number', 'description': 'Minimum price for the stay'}, 'maxPrice': {'type': 'number', 'description': 'Maximum price for the stay'}, 'cursor': {'type': 'string', 'description': 'Base64-encoded string used for Pagination'}, 'ignoreRobotsText': {'type': 'boolean', 'description': 'Ignore robots.txt rules for this request'}}, 'required': ['location']}, response_format='content_and_artifact', coroutine=<function convert_mcp_tool_to_langchain_tool.xx),
>
> StructuredTool(name='airbnb_listing_details', description='Get detailed information about a specific Airbnb listing. Provide direct links to the user', args_schema={'type': 'object', 'properties': {'id': {'type': 'string', 'description': 'The Airbnb listing ID'}, 'checkin': {'type': 'string', 'description': 'Check-in date (YYYY-MM-DD)'}, 'checkout': {'type': 'string', 'description': 'Check-out date (YYYY-MM-DD)'}, 'adults': {'type': 'number', 'description': 'Number of adults'}, 'children': {'type': 'number', 'description': 'Number of children'}, 'infants': {'type': 'number', 'description': 'Number of infants'}, 'pets': {'type': 'number', 'description': 'Number of pets'}, 'ignoreRobotsText': {'type': 'boolean', 'description': 'Ignore robots.txt rules for this request'}}, 'required': ['id']}, response_format='content_and_artifact', coroutine=<function convert_mcp_tool_to_langchain_tool.xx)]

#### 121. Create LangGraph Agent with Airbnb MCP Server Tools

Because tools are accquired asynchronously, we should define our agent using `async` keyword.

```python
async def agent_node(state: AgentState):
    TOOLS = await get_tools()
    llm_with_tools = llm.bind_tools(tools=TOOLS)

    response = llm_with_tools.invoke(state["messages"])

    return {"messages": [response]}
```

> Enter your query (or '/exit' to quit): Help me to find best hotels in London. I would like to check in at 23rd March, 2026 and only stay for 2 nights. Two peoples only, both are adult. I would like to book a slightly higer priced room.
>
> This agent called tool: airbnb_search with args: {'adults': 2, 'checkin': '2026-03-23', 'checkout': '2026-03-25', 'location': 'London, UK', 'maxPrice': 1000, 'minPrice': 300}
>
> [AGENT] generating responses...
> ================================== Ai Message ==================================
>
> It seems there are no available listings for your specified dates and location. Here are a few suggestions:
>
> 1. **Check Dates**: Ensure the check-in/check-out dates are correct. Sometimes future dates may have limited availability.
> 2. **Broaden Location**: Try a more general location like "London, UK" or specific areas like "Central London."
> 3. **Adjust Price Range**: If "slightly higher priced" is flexible, try widening the price range or checking nearby areas.
> 4. **Alternative Booking Platforms**: Consider platforms like Booking.com or Expedia for additional options.
>
> Would you like to refine your search further?

#### 123. Performance Testing of Airbnb MCP Server with LangChain MCP Client in Jupyter

(Skipped)
