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

Here, we choose [Phi-3-mini-4k-instruct-bnb-4bit](https://huggingface.co/unsloth/Phi-3-mini-4k-instruct-bnb-4bit) on purpose, because of its relatively small size.

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

###### Add LoRA Adapters

```python
# Add LoRA adapters
model = FastLanguageModel.get_peft_model(
    model,
    r=64,  # LoRA rank - higher = more capacity, more memory
    target_modules=[
        "q_proj", "k_proj", "v_proj", "o_proj",
        "gate_proj", "up_proj", "down_proj",
    ],
    lora_alpha=128,  # LoRA scaling factor (usually 2x rank)
    lora_dropout=0,  # Supports any, but = 0 is optimized
    bias="none",     # Supports any, but = "none" is optimized
    use_gradient_checkpointing="unsloth",  # Unsloth's optimized version
    random_state=3407,
    use_rslora=False,  # Rank stabilized LoRA
    loftq_config=None, # LoftQ
)
```

###### Set Up the Trainer

```python
from trl import SFTTrainer
from transformers import TraningArguments

# Training arguments optimized for Unsloth
trainer = SFTTrainer(
    model=model,
    tokenizer=tokenizer,
    train_dataset=dataset,
    dataset_text_field="text",
    max_seq_length=max_seq_length,
    dataset_num_proc=2,
    args=TrainingArguments(
        per_device_train_batch_size=2,
        gradient_accumulation_steps=4,  # Effective batch size = 8
        warmup_steps=10,
        num_train_epochs=3,
        learning_rate=2e-4,
        fp16=not torch.cuda.is_bf16_supported(),
        bf16=torch.cuda.is_bf16_supported(),
        logging_steps=25,
        optim="adamw_8bit",
        weight_decay=0.01,
        lr_scheduler_type="linear",
        seed=3407,
        output_dir="outputs",
        save_strategy="epoch",
        save_total_limit=2,
        dataloader_pin_memory=False,
    ),
)
```

###### Train the Model

A LLM can be trained by a single line of code in unsloth, as shown below.

The training time depends on the training data size and configuration.

```python
# Train the model
trainer_stats = trainer.train()
```

Results:

```
==((====))==  Unsloth - 2x faster free finetuning | Num GPUs used = 1
   \\   /|    Num examples = 500 | Num Epochs = 3 | Total steps = 189
O^O/ \_/ \    Batch size per device = 2 | Gradient accumulation steps = 4
\        /    Data Parallel GPUs = 1 | Total batch size (2 x 4 x 1) = 8
 "-____-"     Trainable parameters = 119,537,664 of 3,940,617,216 (3.03% trained)
```

###### Test the Fine-Tuned Model

```python
# Test the fine-tuned model
FastLanguageModel.for_inference(model) # Enable native 2x faster inference

# Test prompt
messages = [
    {"role": "user", "content": "Extract the product information:\n<div class='product'><h2>iPad Air</h2><span class='price'>$1344</span><span class='category'>audio</span><span class='brand'>Dell</span></div>"},
]

inputs = tokenizer.apply_chat_template(
    messages,
    tokenize=True,
    add_generation_prompt=True,
    return_tensors="pt",
).to("cuda")

# Generate response
outputs = model.generate(
    input_ids=inputs,
    max_new_tokens=256,
    use_cache=True,
    temperature=0.7,
    do_sample=True,
    top_p=0.9,
)

# Decode and print
response = tokenizer.batch_decode(outputs)[0]
print(response)
```

Here, we can see that a pretty formatted answer is created by this fine-tuned LLM.

> Message: 'The attention mask API under `transformers.modeling_attn_mask_utils` (`AttentionMaskConverter`) is deprecated and will be removed in Transformers v5.10. Please use the new API in `transformers.masking_utils`.' Arguments: (<class 'FutureWarning'>,) <|user|> Extract the product information: <div class='product'><h2>iPad Air</h2><span class='price'>$1344</span><span class='category'>audio</span><span class='brand'>Dell</span></div><|end|><|assistant|> {"name": "iPad Air", "price": "$1344", "category": "audio", "manufacturer": "Dell"}<|end|>

###### Download Model

Google Colab can save the fine-tuned model in Google Drive, then, we can manually download it in our computer.

```python
model.save_pretrained_gguf("gguf_model", tokenizer, quantization_method="q4_k_m")

gguf_files = [f for f in os.listdir("gguf_model") if f.endswith(".gguf")]
if gguf_files:
    gguf_file = os.path.join("gguf_model", gguf_files[0])
    print(f"Downloading: {gguf_file}")
    files.download(gguf_file)
```

```
Unsloth: Merge process complete. Saved to `/content/gguf_model`
Unsloth: Converting to GGUF format...
==((====))==  Unsloth: Conversion from HF to GGUF information
   \\   /|    [0] Installing llama.cpp might take 3 minutes.
O^O/ \_/ \    [1] Converting HF to GGUF f16 might take 3 minutes.
\        /    [2] Converting GGUF f16 to ['q4_k_m'] might take 10 minutes each.
 "-____-"     In total, you will have to wait at least 16 minutes.

Unsloth: Installing llama.cpp. This might take 3 minutes...
Unsloth: Updating system package directories
Unsloth: Cloning llama.cpp repository...
Unsloth: Building llama.cpp - please wait 1 to 3 minutes
Unsloth: Successfully installed llama.cpp!
Unsloth: Preparing converter script...
WARNING:unsloth_zoo.llama_cpp:Unsloth: Qwen2MoE num_experts patch target not found.
Unsloth: [1] Converting model into f16 GGUF format.
This might take 3 minutes...
Unsloth: Initial conversion completed! Files: ['gguf_model_gguf/phi-3-mini-4k-instruct.F16.gguf']
Unsloth: [2] Converting GGUF f16 into q4_k_m. This might take 10 minutes...
Unsloth: Model files cleanup...
Unsloth: All GGUF conversions completed successfully!
Generated files: ['gguf_model_gguf/phi-3-mini-4k-instruct.Q4_K_M.gguf']
Unsloth: example usage for text only LLMs: /root/.unsloth/llama.cpp/llama-cli --model gguf_model_gguf/phi-3-mini-4k-instruct.Q4_K_M.gguf -p "why is the sky blue?"
Unsloth: Saved Ollama Modelfile to gguf_model_gguf/Modelfile
Unsloth: convert model to ollama format by running - ollama create model_name -f gguf_model_gguf/Modelfile
{'save_directory': 'gguf_model',
 'gguf_directory': 'gguf_model_gguf',
 'gguf_files': ['gguf_model_gguf/phi-3-mini-4k-instruct.Q4_K_M.gguf'],
 'modelfile_location': 'gguf_model_gguf/Modelfile',
 'want_full_precision': False,
 'is_vlm': False,
 'fix_bos_token': False}
```

#### Step 4: Model Setup in Ollama

Ollama: [Importing a model](https://docs.ollama.com/import)

Ollama: [Modelfile](https://docs.ollama.com/modelfile)

###### Examination of Downloaded Model

A `.gguf` file will be created after downloading in your computer.

Before starting using this model, we should create a `Modelfile` in the same directory of our `.gguf` file.

###### Create Modelfile

A `Modelfile` defines a custom configuration of the model.

```
FROM ./unsloth.Q4_K_M.gguf

PARAMETER temperature 0.7
PARAMETER top_p 0.9
PARAMETER stop "<|end_of_text|>"
PARAMETER stop "<|user|>"

TEMPLATE """<|user|>
{{ .Prompt }}<|assistant|>
"""

SYSTEM """You are a helpful AI assistant"""
```

###### Run Fine-Tuned Model in Ollama

After creating Modelfile, we can simply add our fine-tuned model in one line, with `-f` option to identify which Modelfile (configuration) you would like to use.

```bash
ollama create html-model -f Modelfile

ollama run html-model
```

Then, use the same prompt to test our model:

> Prompt: Extract the product information:\n<div class='product'><h2>iPad Air</h2><span class='price'>$1344</span><span class='category'>audio</span><span class='brand'>Dell</span></div>
>
> Answer: {"name": "iPad Air", "price": "$1344", "category": "audio", "manufacturer": "Dell"}

## Fine-Tuning Text Embedding Model

Youtube: [Fine-Tuning Text Embeddings For Domain-specific Search (w/ Python)](https://www.youtube.com/watch?v=hOLBrIjRAj4)

#### Overview

`Embedding models` represent text as **semantic meaningful vectors**.

However, general embedding models can have poor performance on domain-specific texts.

This problem are supposed to be overcome by fine-tuning.

Text embedding becomes more popular in these days with the widespread usage of RAG (Retrieval Augumented Generation).

The core concept of RAG is to improve llm based systems by retrieving relevant content when prompt is provided.

#### The Problem in RAG

###### RAG: Flows

Typical RAG are executed as follows:

1. User raise a query
2. Context retrieval
   - In stead of give the query directly to LLM, context (relevant information) are combined and feeded to LLM to generate response
   - A `vector database` is expected, in which chunks of knowledge (PDFs, etc) are represented as semantic meaningful vectors
   - When query comes in, it is embeded and do `similarity search`, in order to find relevant knowledge.

###### Similar Contents vs. Helpful Info

However, this kind of context retrieval has one **key problem**: `Similarity does not mean helpful.`

For example:

> Query: How do I update my payment method?
>
> Results (similarity search): "To view your payment history, visit the Billing section of your account", "Payment can be made by debit card, and mobile payments."

In the example above, results are semantically similar to user's query, however, they are not answering this query.

Futher, a single phrase can have different meanings in domain-specific scenarios.

> Query 1: What is RAG?
>
> Query 2: What is fine-tuning?

- In comment classifier, the vector representing these two query should be **similar**, to categorize these two queries together.
- In (AI-related) FAQ search, they should be **dissimilar**, because fine-tuning is not helpful for users who would like to know about RAG
- In PM Doc Search, RAG is not standing for retrieval augmented generation, but for red amber and green, the vectors should be **dissimilar** and have more distance than AI related areas.

To solve this problem, we can overcome this by fine-tuning our model for a specific use case.

#### Fine-tuning Embeddings

The basic idea of `fine-tuning` is to adapt a model to a paticular usecase through addition training.

Firstly, we need a `Base model`, and refine this model.

###### 5 Steps for Fine-tuning Embeddings

1. Gather positive (and negative) pairs
2. Pick a pre-trained model
3. Pick a loss function
4. Fine-tune the model
5. Evaluate the model

#### Example: Fine-tuning Embeddings on AI Jobs

###### Step 1: Gather Positive-negative Pairs

Dataset: [ai-job-embedding-finetuning](https://huggingface.co/datasets/shawhin/ai-job-embedding-finetuning)

| Query                                                                   | Positive Match                                                                                                            | Negative Match                                                                                                                                             |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Data pipeline management, advanced SQL techniques, ETL/ELT processes." | Make your impact within a rapidly growing Fintech Company. Build and mange robust data pipelines that support scalable... | Collaborate to design and implement end-to-end AI and data science lifecycle, from data collection and preprocessing to model deployment and monitoring... |

###### Step 2: Pick a Pre-trained Model

To pick the model, a sentence transformer library, [SBERT.net](https://sbert.net/), is used in our example.

`sentence-transformers/all-distilroberta-v1` is selected in our example.

###### Step 3: Pick a Loss Function

In our example, data is structured similiar to `(anchor, positive, negative) triplets`, so loss function of `MultipleNegativesRankingLoss` is selected.

###### Step 4: Fine-Tune Model

###### Step 5: Evaluate the Model

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

## Open Source Models

#### OlmOCR

Home Page: [olmOCR 2](https://olmocr.allenai.org/)

Ai2 : [Main Page](https://allenai.org/)

Hugging Face: [olmOCR-7B-0225-preview](https://huggingface.co/allenai/olmOCR-7B-0225-preview)

Youtube: [olmOCR - The Open OCR System](https://www.youtube.com/watch?v=38loqDtlLok&t=65s)

Allen AI is trying to make things in LLM more open.

They not only release the models that are open-weights, but also probably the only group that doing open-source.

The problem they would like to address is that when you train your LLM, **high-quality** data is essential to you.

Plain text is the only way to get into your training process, however, there are a huge amount of high-quality data that are stored in PDF.

###### What Should We Know about OlmOCR?

- olmOCR is built on top of [Qwen2-VL-7B-Instruct](https://huggingface.co/Qwen/Qwen2-VL-7B-Instruct).
  - The fine-tuning code is relase at [train.py](https://github.com/allenai/olmocr/blob/main/olmocr/train/train.py)
- It can hanlde hand-writting
- Support **markdown** output, so it can handle equations, etc.

## Open Weight Models

#### Mistral Small 3

Mistral: [Mistral Small 3](https://mistral.ai/news/mistral-small-3)

Ollama Library: [mistral-small](https://ollama.com/library/mistral-small)

Hugging Face: [Mistral Small 24B Base](https://huggingface.co/mistralai/Mistral-Small-24B-Base-2501)

Youtube: [Mistral Small 3 - The NEW Mini Model Killer](https://www.youtube.com/watch?v=nCXTdcggwkM)

Open-source actually advance things, just like the release of DeepSeek-R1, because people are able to get access to them, learn from them, and fine-tune them.

Likely, Mistral Small 3 was released in Apache 2.0 license, with its Base and Instruct version. It means that users can easily fine-tune them and deploy them wherever they would like.

- **24B** parameters
- Aiming at replacing models like Llama 3.3 70B, Qwen 32B, and GPT40-mini
- **Agentic-features**: function calling, JSON outputs, etc.

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

## Proprietary Model

#### Gemini Embedding 2

Google: [Gemini Embedding 2: Our first natively multimodal embedding model](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-embedding-2/)

Google Cloud: [Gemini Embedding 2](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/embedding-2)

###### Overview

In previous embedding models, when dealing with inputs in various formats (text, image, audio, video, pdf, etc. ) it is usually ended up to using **multiple vector stores** with different embedding models.

As a result, the searching system would become sophisticated and slow.

`Gemini Embedding 2` is the first natively multimodal embedding model, which not only cover text and images, but also videos (up to 2 minitutes) and audios, and embed them **without** convert their format.

Basically, Gemini Embedding 2 model allows us to represents text, video, audio and pdf in **UNIFIED** embedding spaces, as a vector (a list of number)

- Gemini Embedding 2 captures the **semantic** meaning of a piece of content
- For example, a text ("A cat on a mat"), an image (Photo of cat), and a piece of audio (something saying cat) will be in roughly the same location of embedding space
- Then, when we do similarity search, there is no need to use one model for one modality, instead, we can have any input and retrieve output in different format

#### Claude Sonnet 4.6

Youtube: [Claude Sonnet 4.6 Is Insane, But Here's The Truth Nobody's Telling You.](https://www.youtube.com/watch?v=DyoKuKYEv_U)

Anthropic: [Introducing Claude Sonnet 4.6](https://www.anthropic.com/news/claude-sonnet-4-6)

###### What Sonnet 4.6 Actually Is?

- Anthropic's second major model (after Opus), but cost less
- **1 million token** context window
- The free version of Claude now runs on this model.
- Dropped with ChatGPT Codex 5.3 at the same day

#### Opus 4.6

Youtube: [GPT-5.3-Codex and Opus 4.6 in 6 min..](https://www.youtube.com/watch?v=_zA8aImw-9Y&t=55s)

Anthropic: [Introducing Claude Opus 4.6](https://www.anthropic.com/news/claude-opus-4-6)
