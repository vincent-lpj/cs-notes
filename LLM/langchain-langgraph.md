[ Master Langchain v1 and Ollama - Chatbot, RAG and AI Agents](https://www.udemy.com/course/ollama-and-langchain/)

[Master LangGraph v1 and Ollama - Build Gen AI Agents](https://www.udemy.com/course/langgraph-with-ollama/)

## Section 1: Introduction

#### 1. Welcome & Course Overview

###### Object

- Build generative AI agents using LangGraph and Ollama.
- Learn how modern AI agent work

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

**Important**: `Annotated` must be using in `messages`, in order to let framework read and automatically append messages, instead of overwriting it.

```python
from typing import TypedDict, Annotated
from langgraph.graph import StateGraph, START, END
from langchain_ollama import ChatOllama
from langchain_core.messages import SystemMessage, HumanMessage
from pydantic import BaseModel, Field

# Configuration
BASE_URL = "http://localhost:11434"
MODEL_NAME = "deepseek-r1"

llm = ChatOllama(model=MODEL_NAME, base_url=BASE_URL)
```
