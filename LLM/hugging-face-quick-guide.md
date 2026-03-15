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

## Section 2: Working with Transformers in Hugging Face

#### 6. Tokenizer Fundamentals

In previous sections, we briefly touched on how to use **models** in transfromers library.

In this section, we will have a closer look at **Tokenizer**.

###### Using Pretrained Model

Hugging Face: [Model Card](https://huggingface.co/sshleifer/distilbart-cnn-12-6)

`Tokenizer`, by **itself**, will take in some **text** and output **token IDs**.

```python
from transformers import AutoTokenizer

# Load the tokenizer for the distilbart-cnn-12-6 model
tokenizer = AutoTokenizer.from_pretrained("sshleifer/distilbart-cnn-12-6")

raw_input = [
    "I love deep learning!",
    "I hate it so much!"
]

# Tokenize the input text
inputs = tokenizer(raw_input, padding=True, truncation=True, return_tensors="pt")
print(inputs)
```

Results:

- **tensors** representing two sentences in raw_input, and **attention_mask** will be the output
- `attention mask` tells the model which **token** to pay attention to.
  - `0` means do **NOT** pay attention to, because a **padding token** is added to the end of the first sentence's tokens (`1`)
  - `padding token` does not have semantic meaning
  - The token lists are expected to be **same size**
- `0` means the beginning of sentence, and `2` means the end of sentence

> {'input_ids': tensor([[0,  100,  657, 1844, 2239,  328,    2,    1],        [   0,  100, 4157,   24,   98,  203,  328,    2]]), 'attention_mask': tensor([[1, 1, 1, 1, 1, 1, 1, 0],        [1, 1, 1, 1, 1, 1, 1, 1]])}

###### A Closer Look at Tokenized Sentences

```python
print("Tokenizer output for 'I love deep learning!':")
print(f"Input IDs: {inputs['input_ids'][0]}")
print(f"Attention Mask: {inputs['attention_mask'][0]}")
print("-"*100)
print("Tokenizer output for 'I hate it so much!':")
print(f"Input IDs: {inputs['input_ids'][1]}")
print(f"Attention Mask: {inputs['attention_mask'][1]}")
print("-"*100)

# Tokenize the first sentence along
tokenizer("I love deep learning!", return_tensors="pt")
```

Results:

We will see there is no `1`, which is padding token here in the tensor. And attention mask will be all `1`.

```
Tokenizer output for 'I love deep learning!':
Input IDs: tensor([   0,  100,  657, 1844, 2239,  328,    2,    1])
Attention Mask: tensor([1, 1, 1, 1, 1, 1, 1, 0])
----------------------------------------------------------------------------------------------------
Tokenizer output for 'I hate it so much!':
Input IDs: tensor([   0,  100, 4157,   24,   98,  203,  328,    2])
Attention Mask: tensor([1, 1, 1, 1, 1, 1, 1, 1])
----------------------------------------------------------------------------------------------------{'input_ids': tensor([[   0,  100,  657, 1844, 2239,  328,    2]]), 'attention_mask': tensor([[1, 1, 1, 1, 1, 1, 1]])}
```

###### Tokenizers Under the Hood

```python
# Tokenize the input text into tokens -> list of strings
tokens = tokenizer.tokenize("I love deep learning!")
print(f"Tokens: {tokens}")

# Convert tokens to token IDs -> list of integers
token_ids = tokenizer.convert_tokens_to_ids(tokens)
print(f"Token IDs: {token_ids}")

# Convert token IDs back to tokens -> list of strings
tokens_from_ids = tokenizer.convert_ids_to_tokens(token_ids)
print(f"Tokens from IDs: {tokens_from_ids}")

# Decode token IDs back to text -> string
decoded_tokens = tokenizer.decode(token_ids)
print(f"Decoded Tokens: {decoded_tokens}")

# Decode special tokens (e.g., [CLS], [SEP], [PAD]) back to text
decoded_special_tokens = tokenizer.convert_ids_to_tokens([0, 1, 2])
print(f"Decoded Special Tokens: {decoded_special_tokens}")
```

Results

- Here, the tokens' IDs are the same as previous ones ([ 0, 100, 657, 1844, 2239, 328, 2, 1])
- Except, there is no `0` for begining of sentence, and `2` for the end of sentence
- Also, because this sentence is tokenized alone, so no padding token `1` is added.
- `Ġ` means space in front of a token

> Tokens: ['I', 'Ġlove', 'Ġdeep', 'Ġlearning', '!']
>
> Token IDs: [100, 657, 1844, 2239, 328]
>
> Tokens from IDs: ['I', 'Ġlove', 'Ġdeep', 'Ġlearning', '!']
>
> Decoded Tokens: I love deep learning!
>
> Decoded Special Tokens: ['\<s>', '<pad>', '</s>']

###### Reference

Udemy: [Learn Hugging Face for Mastering Generative AI with LLMs](https://www.udemy.com/course/mastering-generative-ai-with-llms-a-hugging-face-guide/#overview)

Hugging Face: [LLM Course](https://huggingface.co/learn/llm-course/chapter0/1)
