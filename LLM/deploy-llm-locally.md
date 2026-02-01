###### Reference

[Local LLM via Ollama & LM Studio - The Practice Guide](https://www.udemy.com/course/running-open-llms-locally-practical-guide/)

[Ollama](https://ollama.com/)

[LM Studio](https://lmstudio.ai/)

## 1. Introduction

#### 1. Welcome To The Course

This course's object is to run Open AI models in your local computer.

Hardware requirement

How to leverage LM Studio and Ollama

#### 2. What Exactly are Open LLMs?

###### Which Part of LLM is Open?

Training algorithm / Code ---> Model Weights / Parameters

An open Large Language Model is a LLM whose weight (parameters) are publically released under a specific license.

###### Understanding Models Parameters & Sizes

LLM model is basically `statistic models` that generate tokens and assign probabilities to them, based on the input we fed into them.

User's `Input Prompt` is deconstructed into `tokens` (token IDs), and then, then trained model will output tokens (token IDs) and translate it to `human-readable` text.

#### 3. Why Would You Want to Run Open LLMs Locally?

In this course, we will learn hardware requirements.

Open vs Proprietary LLMs?

https://arena.ai/zh/leaderboard

Open LLM

- Free to use
- 100% privacy, can be run locally or on your servers
- No vender lock-in, full control
- Offline-first, low/no latency

Proprietary LLMs

- Paid
- Hosted by provider
- Possible vender lock-in
- Internet connection required

#### 4. Popular Open LLMs - Some Examples

[Meta's Llama Models](https://www.llama.com/)

[Google's Gemma Models](https://deepmind.google/models/gemma/)

[Deepseek Models](https://www.deepseek.com/)

[Some Mistral Models](https://mistral.ai/models)

#### 5. Where to Find Open LLMs?

[Hugging Face](https://huggingface.co/) is the defecto place to go, when you would like to get a general overview of avaiable models and find new models.

There is also a [catalog](https://huggingface.co/models) of models.

Click model card to know more about Open LLMs,

#### 6. Running LLMs Locally - Available Options

- [Llama.cpp](https://github.com/ggml-org/llama.cpp)
  - The following two solutions are wrappers of Llama.cpp
  - Very low level solution
- LM Studio
  - User-friendly GUI
  - No technical expertise required
- Ollama
  - User-friendly CLI
  - Only techinical expertise required

#### 7. Check the Model Licenses!

For example, [Gemma](https://ai.google.dev/gemma/terms) license here.

MIT/Apache 2.0: very permissive license, allow private & commercial use without permission

Llama: somewhat permissive license, allow private & commercial use with limitations

Gemma: somewhat permissive license, allow private & commercial use with special requirements

## 2. Understanding Hardware Requirements & Quantizetion

#### 10. Module Introduction

Hardware Requirements & Quantization

In this section, we will get to know why model parameters (sizes) matter, what hardware is required for running LLMs, and how quantization help us lower this requirement without largely influence its performance.

#### 11. LLM Hardware Requirements - First Step

This process,

Input Prompt -> Trained Model -> Output Response

where LLM is used to generate output, is called **inference**.

This inference process, musted be **hosted** somewhere, it can be hosted in your local machine.

Model should be **executed by GPU (or CPU)**, and **loaded into VRAM (or RAM)** .

You should load the entire parameters and context window into memory during LLM execution.

#### 12. Deriving Hardware Requirements From Model Parameters

This [Online Tokenizer](https://tiktokenizer.vercel.app/) show how user's input prompt is transformed into tokens.

When loading a LLM, we load all the weights (parameters) into VRAM (or RAM).

Every parameters is a float32 or float16 value (e.g. 0.512913), and takes up 4 or 2 bytes of memory.

So, a 2bn model takes up 4~8 GB of memory.

#### 13. Quantization To The Rescue!

The technique of Quantization helps us running bigger models on personal machines, by reducing memory requirements.

Basically, we run quantized model in our local machine and rent servers.

In quantized models, parameter values have been transformed from **float16/32 to Int4/8**.

Model shared on Hugging Face, and run in LM Studio and Ollama, are available as quantized versions.

For example, in the Model Tree for google/gemma-3-27b-it, we can find different quantization versions of this model.

GGUF files.

#### 14. Does It Run On Your Machine?

Preferably, you should have GPU and VRAM, but CPU and RAM will also work.

Hugging Face, as well as LM studio can help you find out if a model is suitable for your local machine.

## 3. LM Studio Deep Dive

#### 15. Module Introduction

LM Studio is a convinient chat interface for running open models locally.

#### 16. Running Locally vs. Remotely

In this course, we will focus on running models locally, instead of remote server.

#### 17. Install & Using LM Studio

[LM Studio](https://lmstudio.ai/)

After installing LM studio, you should be able to find a chat window, a chat list, and a model loader in LM Studio.

Also, you can switch between different mode (developer, for example).

#### 18. Finding, Downloading & Activating Open LLMs

On Hugging Face, under `Use this model` dropdown here, you can find if a model supports LM Studio.

In `Model Search`, you can find a list of available models. A large portion of models here are quantized.

Here, we download `Gemma 3 12B Instruct QAT`.

When running this model, in `Setting` -> `Hardware`, we can see System Resource Usage,

for example, how much RAM or CPU is used during execution.

#### 19. Using the LM Studio Chat Interface

We can click on the button on the left, to create a new `chat session` .

Also, we can control the message generated by `regenerate`, `delete`, `copy`, etc.

`System Prompt` can also be edited to control the model’s behavior.

In `Setting` -> `Papearance`, we can change chat style of LM Studio.

#### 20. Working with System Prompts & Presets

System Prompts and Presets can be seen in the `right` sidebar.

#### 21. Managing Chats

Using `...` in the left sidebar, you can reveal the chat in finder, we can find that chats are simply stored in `JSON`.

Chats can be sorted by creating folders.

#### 22. Power User Features for Managing Models & Chats

For example, we can `Branch chat after this message` and create parralel chat history.

`Model Load Settings` on the top of the window, where you can adjust context length ,etc.

`Web Endpoint` and `Debug Logs` in developer page.

`Models` in which you can see LLMs downloaded.

#### 23. Leaveraging Multimodal Models & Extracting Contents from Images (OCR)

To work with images (which you can attach in the `+` button), you should have a `multimodal` model.

Then, using `attach images` to interact with your LLMs.

#### 24. Analyzing & Summarizing PDF Documents

LLM can also process other types of files, such as pdf.

However, because of context window limits, the ability to process files can differ.

#### 25. Onwards To More Advanced Settings

We have looked at the System Prompt and Preset in previous lectures.

Here, we can have a look at more advanced `Model Settings` at the right sidebar of LM Studio.

Those Model Settings can also be saved in `Preset`.

- Temperature: controls how much randomness
- Sampling: Top K, Top P

#### 26. Understanding Temperature, top_k and top_p

To control how an LLM generates tokens, you can adjust **`temperature`**, **`top_k`**, and **`top_p`**.

To understand how these parameters work, it helps to know how an LLM produces **token candidates** during generation.

At each step, the model assigns probabilities to possible next tokens.
For example, given the prompt:

> _“The sky is”_

The model might assign probabilities like:

- **clear** — 12%
- **blue** — 45%
- **visible** — 21%
- **others** — 22%

These parameters determine **which tokens are eligible for selection** and **how their probabilities are used** when sampling the next token.

- **Temperature** modifies the probability distribution:
  - **Low temperature** exaggerates differences between probabilities, making high-probability tokens much more likely (more deterministic).

  - **High temperature** flattens the distribution, making lower-probability tokens more likely (more random).

- **Top-K** limits the number of candidate tokens by keeping only the **K tokens with the highest probabilities**.
  All other tokens are discarded before sampling.

- **Top-P** limits candidate tokens by keeping the **smallest set of tokens whose combined probability is at least \*P\***.
  Tokens outside this cumulative probability mass are discarded.

- **Min-P** discards candidate tokens whose probabilities fall **below a minimum probability threshold**.
  Only tokens with probabilities ≥ _minP_ are eligible for sampling.

#### 27. Controlling Temperature, top_k, top_p in LM Studio

###### Temperature

The default value is `0.1`

When you set `temperature` to zero, and give the exact same input, the same model will return exact the same response.

###### Top_K, Top_P

These two settings can be configured below.

#### 28. Managing the Underlying Runtime & Hardware Configuration

###### Runtime

What underlying tools are needed.

For example, llama.cpp is used in GGUF.

###### Hardware

Check the status of your CPU, GPU, RAM, VRAM.

Here, You can turn off the GPU usage.

#### 29. Managing Context Length

###### Context Length

`Context length` is the maximum amount of data—measured in tokens—a model can process, analyze, and "remember" at one time, acting as its immediate working memory

Note: the context length also takes up your memory, so we **do not** always use the maximum value. For example, if we increase the context length from about 4k to 20k in Gemma 3 12B Instruct QAT model, the memory usage will increase from about 9gb to 15gb.

###### GPU Offload

Usually, we maxmize GPU offload to allow GPU to take over all the jobs.

#### 30. Using Flash Attention

###### Flash Attention

This will decrease the memory usage in some models.

###### K and V Cache Quantization Type

#### 31. Working with Structured Outputs

###### Structured Output

This option force model to generate a structured outputs, `JSON`, at the end of a generation.

This is extremely useful when the output is used in next step of application.

Structured output can be defined as a [JSON Schema](https://json-schema.org/learn/miscellaneous-examples), in Model Parameters.

###### Example

For example, we attach a PDF file of financial report, and give LLM this instructions:

> Return the key data as JSON

Then, we define Structure Output as `JSON schema` like below:

```json
{
  "$id": "https://example.com/person.schema.json",
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "Financial Data",
  "type": "object",
  "properties": {
    "year": {
      "type": "string",
      "description": "The year of the report"
    },
    "revenue": {
      "type": "integer",
      "description": "The total revenue of that year"
    },
    "Operating_Income": {
      "description": "Operating Income of the year",
      "type": "integer"
    }
  }
}
```

LLM would generate answers like this

```json
{
  "year": "2021",
  "revenue": 6875,
  "Operating_Income": 1390
}
```

#### 32. Using Local LLMs for Code Generation

Local LLMs can also help you generate code.

#### 33. Content Generation & Few Shot Prompting (Prompt Engineering)

###### Few Shot Prompting

Few Shot Prompting means that you provide **some examples** for a given task.

> You are an expert LinkedIn post generator.
>
> Here are some example LinkedIn posts I wrote in the past.
>
> <linkedin-article-1>
> ...
>
> <linkedin-article-2>
> ...
>
> Above, you see two example LinkedIn posts I wrote in the past.
>
> Use the same writing style as shown in those posts, but DON'T use the content.
>
> Instead, using the above shown writing styles, generate a new LinkedIn post about "...".
>
> The post should cover the following core concepts & topics:
> ...

#### 34. Onwards To Programmatic Use

Actually, you can use LM Studio **programatically**, which means you can build your own application using locally deployed LLMs.

LM studio, just like OpenAI, exposes a locally running large language model API server.

#### 35. LM Studio & Its OpenAI Compatibility

###### Ways to Access Locally Deployed LLMs

Firstly, `developer mode` should be on, ports can be defined in `settings` besides.

In `Server` page, switch the server to **running**, and you will find a message in the developer logs below.

> 2026-02-01 16:39:50 [INFO] Just-in-time model loading active.

Urls, or api endpoints, and domain are shown below.

**Important**: LM studio server can be reached using **OpenAI SDK**.

```python
from openai import OpenAI

client = OpenAI(
+    base_url="http://localhost:1234/v1"
)

# ... the rest of your code ...

```

#### 36. More Code Examples

```json
from openai import OpenAI

client = OpenAI(
  base_url="http://localhost:1234/v1",
  api_key="something-doesnt-matter",
)

response = client.chat.completions.create(
  model="gemma-3-12b-it-qat",
  messages=[
    {
      "role": "system",
      "content": "You are a helpful and friendly assistant."
    },
    {
      "role": "user",
      "content": "What is the meaning of life?"
    }
  ],
  temperature=0.7,
)

print(response.choices[0].message.content)
```

#### 37. Diving Deeper into the LM Studio APIs

LM studio also offer another API that has different endpoints than the OpenAI compatible one, such as **REST API**.

#### 38. Using the Python / JavaScript SDKs

[LM Studio Python SDK](https://lmstudio.ai/docs/python)

[LM Studio JavaScript (TypeScript) SDK](https://lmstudio.ai/docs/typescript)

## Ollama Deep Dive

## Course Roundup
