#### LLM Provider

AI Arena: [LeaderBoard](https://arena.ai/leaderboard)

Ollama: [Library](https://ollama.com/library)

Hugging Face: [Models](https://huggingface.co/models)

LiteLLM: [Supported Providers & Models](https://docs.litellm.ai/docs/providers)

OpenAI: [Open Models](https://openai.com/open-models/)

Anthropic: [Home](https://www.anthropic.com/)

Google: [Gemini Models](https://ai.google.dev/gemini-api/docs/models)

Llama: [Build the Future](https://www.llama.com/)

DeepSeek: [GitHub Homepage](https://github.com/deepseek-ai)

Qwen: [API Platform](https://qwen.ai/apiplatform)

Mistral AI: [Models](https://mistral.ai/models)

## Open Weight Models

#### GPT-OSS

Open AI: [Introducing GPT-OSS](https://openai.com/index/introducing-gpt-oss/)

Ollama Library: [GPT-OSS](https://ollama.com/library/gpt-oss)

YouTube: [OpenAI's New Open Models - GPT-OSS 120B & 20B](https://www.youtube.com/watch?v=guHW1Eb3xSs)

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
