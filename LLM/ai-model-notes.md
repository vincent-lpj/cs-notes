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
