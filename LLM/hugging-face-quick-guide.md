#### 1. Understanding Large Language Models in Hugging Face

Hugging Face has a lot of built-in functionality that automates process of **building** and **training** LLMs.

Currently, LLMs are built off the **transformer** architecture. Typically, there are two types of transformer.

- Seq2Seq transformer
- Causal LM: just the decoder portion

In LLMs, when you would like to generate a sentence, you

1. put your prompt to the model
2. the model will output a probability distribution of what is the **next best** token
3. the output token with original prompt will be **passed back** to model again
4. the model will output the next best token, and **repeat** this process
5. it is ended when the model output **the end of sentence** token

These transformer models are trained on a large corpus of text, using supervised learning to predict the next word.

Developer will use the difference between the best next token and the token LLM predicted, calculate the loss and update parameters inside models.

**Base LLM** is trained on text, and only trained to **predict the next best token**, it is only good for **autocompletion**.

However, we expect LLM to summarized text, translate text and answer questions, that is when **instruction tuning** comes in.

Some **Instruction Tuned LLM** are fine-tuned by using human scores on the target response using **Reinforcement Learning** from Human Feedback **RLHF**

#### 2. Managing Compute Requirements for LLMs

- Each parameter in an LLM takes up 4 bytes (32-bit precision) just to store the model.
- GPT-3 has 175B parameters = 700GB of GPU RAM, just to store the model
- Converting to 16-bit (FP16) requires 2 bytes per parameter.
- Training a model can use 20 bytes/parameter to store it (optimizer states, gradients, & activations and temp variables)

#### 3. What is Hugging Face?

We are going to be using Hugging Face to be able to work with LLMs.

With Hugging Face, we can use LLMs without knowing much about the underlying architecture of LLMs. And boilerplate codes are not needed if we use Hugging Face.

###### Transformers Library

PyPI: [transformers](https://pypi.org/project/transformers/)

- provides easy-to-use implementation of state-of-the-art NLP models.
- includes BERT, GPT-2, T5, RoBERTa, and more
- Designed for efficiency and ease of use

###### Hugging Face

- Datasets Library
  - text corpora, benchmark datasets, and others
- Model Hub
  - repository of pre-trained models contributed by community
  - easy to download and use models, or contribute your own

#### 4. Accessing Pre-Trained Models from Hugging Face: Hands-On Example

Hugging Face: [GPT-2](https://huggingface.co/docs/transformers/en/model_doc/gpt2?usage=AutoModel)

We are going start with the most popular series of LLMs, the **GPT** model.

In this section, we will figure out how to use GPT to generate text by **pulling down** this GPT model from Hugging Face.

Basically, we can have a look at how to use this model in `Hugging Face -> Use this model -> Transformers`

###### Access Model by Pipeline

Transformers: [Text Generation](https://huggingface.co/docs/transformers/main/en/main_classes/text_generation)

Transformers: [Pipelines](https://huggingface.co/docs/transformers/en/main_classes/pipelines)

A Hugging Face pipeline is a **high-level** abstraction for running inference on models from Hugging Face Model Hub.

It simplifies the process of using pre-trained models for various tasks such as language understanding, computer vision, etc.

`pipeline()` function can easily load models and tokenizers, as well as perform inference without requiring expertise in underlying models.

```python
import torch
from transformers import pipeline

pipeline = pipeline(task="text-generation", model="openai-community/gpt2", dtype=torch.float16, device=0)
pipeline("Hello, I'm a language model", max_new_tokens=30, num_return_sequences=1)
```

> [{'generated_text': "Hello, I'm a language modeler. I like to talk about languages, but I'm also a developer. I'm a very good developer. My job is to make sure I don't forget that I'm a programmer. I write things on a lot of different platforms: Windows, Linux, MacOSX. I have a lot of different projects. I'm a very good developer. I'm a very good developer.\n\nI'm pretty good at programming. I've done pretty much everything I can, and I've done quite a bit of stuff that I've not done. I'm pretty good at programming. I've done pretty much everything I can, and I've done quite a bit of stuff that I've not done.\n\nI've met a lot of people who have worked in this field, and I've met a lot of people who are very good at it. I'm very good at programming. I've done pretty much everything I can, and I've done quite a bit of stuff that I've not done.\n\nI've been doing some of my most important work in this field, and there's still a lot of work to do. I've been doing some of my most important work in this field, and there's still a lot of work to do"}]

###### Access Model Directly

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained("openai-community/gpt2")
tokenizer = AutoTokenizer.from_pretrained("openai-community/gpt2")

# encode context the generation is conditioned on
input_ids = tokenizer("I enjoy walking with my dog.", return_tensors="pt").to(model.device)

output = model.generate(**input_ids, max_new_tokens=40)
# output should be decode at first to be printed
print(tokenizer.decode(output[0], skip_special_tokens=True))
```

> I enjoy walking with my dog. I love to play with my dog. I love to play with my dog. I love to play with my dog. I love to play with my dog. I love to play with my dog.

###### Reference

Udemy: [Learn Hugging Face for Mastering Generative AI with LLMs](https://www.udemy.com/course/mastering-generative-ai-with-llms-a-hugging-face-guide/#overview)
