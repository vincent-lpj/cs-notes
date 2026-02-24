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
