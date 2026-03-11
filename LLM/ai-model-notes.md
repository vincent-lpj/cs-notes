#### LLM Provider

OpenAI: [Open Models](https://openai.com/open-models/)

Anthropic: [Home](https://www.anthropic.com/)

Google: [Gemini Models](https://ai.google.dev/gemini-api/docs/models)

Llama: [Build the Future](https://www.llama.com/)

DeepSeek: [GitHub Homepage](https://github.com/deepseek-ai)

Qwen: [API Platform](https://qwen.ai/apiplatform)

Mistral AI: [Models](https://mistral.ai/models)

#### Useful Tools/Websites

AI Arena: [LeaderBoard](https://arena.ai/leaderboard)

Ollama: [Library](https://ollama.com/library)

Hugging Face: [Models](https://huggingface.co/models)

LiteLLM: [Supported Providers & Models](https://docs.litellm.ai/docs/providers)

OpenRouter: [The Unified Interface for LLMs](https://openrouter.ai/)

#### Libraries

Transformer: [the model-definition framework](https://github.com/huggingface/transformers?tab=readme-ov-file)

PyTorch: [Tensors and Dynamic neural networks](https://github.com/huggingface/transformers?tab=readme-ov-file)

## Fine-Tuning LLMs

Youtube: [EASIEST Way to Fine-Tune a LLM and Use It With Ollama](https://www.youtube.com/watch?v=pTaSDVz0gok)

#### What Fine-Tuning Is?

Fine-Tuning is taking a **pre-trained** language model and **teaching** it to perform better at a specific task.

Instead of training a model from zero, you take a model that already knows human language. Then, you feed them with examples about real use cases.

It is different than parameter tuning, which adjust setting like temperature or `Top_K` to change how the model performs.

###### Three Main Scenarios

- When you need consistent formatting or style and prompting can not achieve
- When you have a lot of domain specific data, the model have not seen before
  - Like medical records, etc.
- When you want to reduce costs by using a relatively small model

#### Goal

###### Prerequisites

Unsloth: [Fine-tuning & Reinforcement Learning for LLMs](https://github.com/unslothai/unsloth)

Unsloth: [Fine-tuning LLMs Guide](https://unsloth.ai/docs/get-started/fine-tuning-llms-guide)

###### What Should We Do Next?

In this tutorial, we will fine-tune a model and teach it to generate a specific format from HTML inputs.

For this tutorial, [unsloth](https://unsloth.ai/) will adopted to do our fine-tuning.

#### Step 1: Gathering Data

The first step you need to fine-tune a model, is always gathering data.

A small dataset that demostrates a **HTML Extraction** will be used in this tutorial. Basically, we will give LLM `Expected Prompt` and `Expected Output` and let it learn from this.

###### Examinition of Data

It is expected that fine-tuned LLM will take HTML formatted string input, and give a nicely formatted output (JSON format).

LLM will be trained on about 500 pairs of inputs and outputs.

```json
  {
    "input": "Extract the product information:\n<div class='product'><h2>Asus ROG Strix</h2><span class='price'>$1106</span><span class='category'>electronics</span><span class='brand'>Amazon</span></div>",
    "output": {
      "name": "Asus ROG Strix",
      "price": "$1106",
      "category": "electronics",
      "manufacturer": "Amazon"
    }
  },
```

#### Step 2: Google Colab Setup

###### What Is Google Colab

Using Google Colab has many merits:

- Free online code editor by Google
- Access to high-end GPUs for model traning
- Train model in Google Colab
- Download trained models to your computer
- Run models locally using Ollama

###### GPU Usage in Google Colab

Of course, we can fine-tune the LLM in our own computer, as well as Google Colab.

In Google Colab, we can change the configuration of `Runtime Type`, such as Python 3, and `Hardware Accelerator`, such as T4 GPU, etc.

To use `CUDA`, we need to have CUDA installed in our system, and own a Nvidia GPU to make it work.

However, with Google Colab, we can simply use `CUDA` without extra configuration.

```python
# For GPU check
import torch
print(f"CUDA available: {torch.cuda.is_available()}")
print(f"GPU: {torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'None'}")
```

As expected, a T4 GPU is loaded with available CUDA.

> CUDA available: True GPU: Tesla T4

###### Examination of Data and Configs

Firstly, the dataset prepared in JSON are loaded as below:

```python
import json

file = json.load(open("json_extraction_dataset_500.json", "r"))
print(file[1])
```

> {'input': "Extract the product information:\n<div class='product'><h2>iPad Air</h2><span class='price'>$1344</span><span class='category'>audio</span><span class='brand'>Dell</span></div>", 'output': {'name': 'iPad Air', 'price': '$1344', 'category': 'audio', 'manufacturer': 'Dell'}}

#### Step 3: Fine-Tuning with Unsloth

Unsloth: [Phi-3 Support](https://unsloth.ai/blog/phi3)

Unsloth: [LoRA Fine-tuning Hyperparameters Guide](https://unsloth.ai/docs/get-started/fine-tuning-llms-guide/lora-hyperparameters-guide)

###### Install Necessary Libraries

```bash
!pip uninstall -y unsloth peft

!pip install unsloth trl peft accelerate bitsandbytes
```

###### Load Model and Tokenizer

In this section, we need to decide which model to pick.

Here, we choose P[hi-3-mini-4k-instruct-bnb-4bit](https://huggingface.co/unsloth/Phi-3-mini-4k-instruct-bnb-4bit) on purpose, because of its relatively small size.

See: [Unsloth Model Catelog](https://unsloth.ai/docs/get-started/unsloth-model-catalog#phi-models)

```python
from unsloth import FastLanguageModel
import torch

model_name = "unsloth/Phi-3-mini-4k-instruct-bnb-4bit"

max_seq_length = 2048  # Choose sequence length
dtype = None  # Auto detection

# Load model and tokenizer
model, tokenizer = FastLanguageModel.from_pretrained(
    model_name=model_name,
    max_seq_length=max_seq_length,
    dtype=dtype,
    load_in_4bit=True,
)
```

###### Format Data

```python
from datasets import Dataset

def format_prompt(example):
    return f"### Input: {example['input']}\n### Output: {json.dumps(example['output'])}<|endoftext|>"

formatted_data = [format_prompt(item) for item in file]
dataset = Dataset.from_dict({"text": formatted_data})
```

###### Set Up the Trainer

```python
from trl import SFTTrainer
from transformers import TraningArguments
```

###### Test the Fine-Tuned Model

###### Download Model

#### Step 4: Model Setup in Ollama

Ollama: [Modelfile](https://docs.ollama.com/modelfile)

###### Examination of Downloaded Model

A `.gguf` file will be created after downloading in your computer.

###### Run Fine-Tuned Model in Ollama

```bash
ollama create html-model -f Modelfile

ollama run html-model
```

## Fine-Tuning Text Embedding Model

Youtube: [Fine-Tuning Text Embeddings For Domain-specific Search (w/ Python)](https://www.youtube.com/watch?v=hOLBrIjRAj4)

## LLM Related Topics

#### Thinking Models

Thinking models, or reasoning models have got a lot of attentions these days.

When you are using thinking models, in addition to the response, you will see a short summary of the contents of the **thinking trace**.

###### How Does Thinking Models Work

- LLM developer saw that **chain-of-thought** prompting can lead to improved performance
- And scaling laws suggest that giving model more compute at test time (to think longer) should improve LLM's ability to provide more correct response
- During **post-training**, we can use reinforcement learning to make models think and reason more effectively to produce more long chains of thought.
- After training, adopt **best-of-n** to increase the chance of correct answer
- Combing these steps, we end up wth **thinking** LLMs, which generate long reasoning traces to arrive at an answer to a user query.

Scaling laws describes how model performances improve as you increase the amount of training data and compute.

###### Chain of Thought Prompting

See: [Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)

Let LLM generate a series of intermediate steps before producing an answer.

Standard Prompting

> Model Input
>
> Q: Roger has 5 tennis balls. He buys 2 more cans of tennis ball. How many tennis balls does he have now?
>
> A: The answer is 11.
>
> Q: The cafeteria had 23 apples. If they used 20 to make lunch and bought 6 more. How many apples do they have?

> A: The answer is 27 X

Chain-of-Though Prompting

> Model Input
>
> Q: Roger has 5 tennis balls. He buys 2 more cans of tennis ball. How many tennis balls does he have now?
>
> A: Roger started with 5 balls. 2 cans of 3 tennis balls each is 6 tennis balls. 5 + 6 = 11. Then answer is 11.r
>
> Q: The cafeteria had 23 apples. If they used 20 to make lunch and bought 6 more. How many apples do they have?

> A: The cafeteria had 23 apples originally. They used 20 to make lunch. So they had 23 - 20 = 3. They bought 6 more apples, so they have 3 + 6 =9.

###### Model Post-Training

In model **pre-training**, we generally train LLM to do next token prediction on massive amount of text.
This is to equip model with a board understanding of patterns, features and relationships with the data.

In post-training, we futher improve quality and adapt the model to more spealized tasks.

Train the model with the output of a chain of thought that leads to the correct answer.

###### Supervised Fine-Tuning (SFT) and Reinforcement Learning (RL)

(To be added)

## Open Weight Models

#### Mistral Small 3

Mistral: [Mistral Small 3](https://mistral.ai/news/mistral-small-3)

Ollama Library: [mistral-small](https://ollama.com/library/mistral-small)

Youtube: [Mistral Small 3 - The NEW Mini Model Killer](https://www.youtube.com/watch?v=nCXTdcggwkM)

#### GPT-OSS

Open AI: [Introducing GPT-OSS](https://openai.com/index/introducing-gpt-oss/)

Ollama Library: [GPT-OSS](https://ollama.com/library/gpt-oss)

Hugging Face: [gpt-oss - a openai Collection](https://huggingface.co/collections/openai/gpt-oss)

YouTube: [OpenAI's New Open Models - GPT-OSS 120B & 20B](https://www.youtube.com/watch?v=guHW1Eb3xSs)

###### Overview

- Two models comes out: 120b and 20b model.
  - 120b model for advanced GPUs

  - 20b model for local deployment, ollama and LM studio, etc.

- Open **weight** models, instead of open **source** models like: [Olmo](https://allenai.org/olmo)
- Compatible with Response API
- Like OpenAI o-series, supports three reasoning efforts - low, medium and high

#### Phi-4

Hugging Face: [Phi-4](https://huggingface.co/microsoft/phi-4)

Ollama Library: [phi4](https://ollama.com/library/phi4)

Microsoft: [Introducing Phi-4: Microsoft’s Newest Small Language Model Specializing in Complex Reasoning](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/introducing-phi-4-microsoft%E2%80%99s-newest-small-language-model-specializing-in-comple/4357090)

Microsoft: [Welcome to the new Phi-4 models - Microsoft Phi-4-mini & Phi-4-multimodal](https://techcommunity.microsoft.com/blog/educatordeveloperblog/welcome-to-the-new-phi-4-models---microsoft-phi-4-mini--phi-4-multimodal/4386037)

YouTube: [Unlock Open Multimodality with Phi-4](https://www.youtube.com/watch?v=qAgAQQ41P3A)

###### Phi-4 Mini

It is noticeable that `phi-4 mini` have the ability of function calling.

So, it means that we can have **local model** for doing function calling at a relatively small size.

The [phi-4-mini-instruct](https://huggingface.co/microsoft/Phi-4-mini-instruct) model is 3.8 billion parameters.

###### Phi-4-multimodal-instruct

Hugging Face: [Phi 4 Multimodal Instruct](https://huggingface.co/microsoft/Phi-4-multimodal-instruct)

In contrast to [phi-3.5-vision-instruct](https://huggingface.co/microsoft/Phi-3.5-vision-instruct), Phi-4-multimodal is actually a full multimodal model. Not only `vision encoder`, but also an `audio encoder` are included in this model.

#### DeepSeek OCR

Official Website: [DeepSeek OCR](https://deepseek-ocr.io/)

Hugging Face: [DeepSeek OCR 2](https://huggingface.co/deepseek-ai/DeepSeek-OCR-2)

Tutorial: [DeepSeek OCR - More than OCR](https://www.youtube.com/watch?v=YEZHU4LSUfU)

###### What Task It can Perform

- **📝 Free OCR**: Extracts raw text from the image.
- **📄 Convert to Markdown**: Converts the document into Markdown, preserving structure.
- **📈 Parse Figure**: Extracts structured data from charts and figures.
- **🔍 Locate Object by Reference**: Finds a specific object/text.

###### Related Topics:

Computer Vision: [OpenCV](https://opencv.org/)

Azure: [Document Intelligence](https://azure.microsoft.com/en-us/products/ai-foundry/tools/document-intelligence)

###### How Images in Transformer Work

Even images are expected to be **tokenized** to work in transformer.

See: [Vision Transformer](https://en.wikipedia.org/wiki/Vision_transformer)

- Cut images into patches.

- Patches are converted individually into tokens

###### Uniqueness of DeepSeek-OCR

DeepSeek-OCR is not just for OCR.

Core Engine: [DeepEncoder](https://huggingface.co/deepseek-ai/DeepSeek-OCR/blob/main/deepencoder.py)

DeepSeek-OCR uses [vision token](https://huggingface.co/blog/onekq/behind-each-token) to represent text tokens.

It introduces Contexts Optimal Compression, so that we can use vision to compress text.

- Store tokens (text) in images
- Then decode these images to text token with 97% accuracy
- 50 vision tokens for 1000 text tokens
- New form of memory
  - e.g. Conversation History -> vision tokens

#### Claude Sonnet 4.6

Youtube: [Claude Sonnet 4.6 Is Insane, But Here's The Truth Nobody's Telling You.](https://www.youtube.com/watch?v=DyoKuKYEv_U)

Anthropic: [Introducing Claude Sonnet 4.6](https://www.anthropic.com/news/claude-sonnet-4-6)

###### What Sonnet 4.6 Actually Is?

- Anthropic's second major model (after Opus), but cost less
- 1 million token context window
- The free version of Claude now runs on this model.
- Dropped with ChatGPT Codex 5.3 at the same day

#### Opus 4.6

Youtube: [GPT-5.3-Codex and Opus 4.6 in 6 min..]()

Anthropic: [Introducing Claude Opus 4.6](https://www.anthropic.com/news/claude-opus-4-6)
