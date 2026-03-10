# PyTorch

## Introduction

#### Start Point

`Neual Network` are often trained by the following three lines of code, from GPT-4 to student's assignment.

```python
loss.backward()
optimizer.step()
optimizer.zero_grad()
```

#### The 5-Step Deep Learning Recipe

In this tutorial, we will go through the following five steps using simplified examples.

| Step              | Concept (Math)              | From Scratch (Raw Tensors)          | Professional (`torch.nn`)  |
| ----------------- | --------------------------- | ----------------------------------- | -------------------------- |
| 1. Prediction     | Make a prediction:          | y_hat = X @ W + b                   | y_hat = model(x)           |
| 2. Loss Calc      | Quantify the error:         | loss = torch.mean((y_hat - y)\*\*2) | loss = criterion(y_hat, y) |
| 3. Gradient Calc  | Find the slope of the loss: | loss.backward()                     | loss.backward()            |
| 4. Param Update   | Step down the slope:        | w -= lr \* w.grad                   | optimizer.step()           |
| 5. Gradient Reset | Reset for the next loop.    | w.grad.zero\_()                     | optimizer.zero_grad()      |

## Data Structure in PyTorch

In PyTorch, `torch.Tensor` is the only data structure you will need.

#### Creation of torch.Tensor

`Tensor` is simliar to multi-dimensional array in Numpy, in the first look.

###### Pattern 1: Direct Creation from Data (List)

```python
import torch

# Input: A standard Python List
data = [[1, 2, 3], [4, 5, 6]]
my_tensor = torch.tensor(data) # return a Tensor object

print(my_tensor)
```

> tensor([[1, 2, 3],

        	[4, 5, 6]])

###### Pattern 2: Creation from A Desired Shape

When **initializing** our model weights, usually we know the shape, but not the **values** yet.

Thus, we

- Decide the shape first (Python `tuple` object)
- Create tensor that fits this shape
  - all `1`
  - all `0`
  - all random numbers

```python
# Partern two: creation from a desired shape
# two-dimensional tensor with 2 rows and 3 columns
shape = (2, 3)

# Create a tensor of the desired shape filled with all zeros or all ones, or with random values
ones = torch.ones(shape)
zeros = torch.zeros(shape)
random = torch.rand(shape) # random values between 0 and 1
```

###### Pattern 3: Creation by Mimicking Another Tensor

Sometimes, you would like to have a tensor that has the exact shape and dtype as another one.

Instead of creating a tensor manually, we can just **mimic** it.

```python
# Partern 3: Creation by mimicking another tensor
# Input: A `template` tensor
template = torch.tensor([[1, 2], [3, 4]])

# Create a new tensor with the same properties (shape and datatype) as the `template` tensor
rand_like = torch.rand_like(template, dtype=torch.float) # random values between 0 and 1, with the same shape as `template`

print(f"Template tensor:\n{template}\n")
print(f"Random tensor with same shape:\n{rand_like}\n")
```

#### Inside Tensor: Shape, Type and Device

###### Overview of 3 Critical Attributes

```python
import torch

tensor = torch.randn(3, 4)

print(f"Shape: {tensor.shape}")
print(f"Datatype: {tensor.dtype}")
print(f"Device: {tensor.device}")
```

Results:

> Shape: torch.Size([3, 4])
> Datatype: torch.float32
> Device: cpu

###### Breakdown of 3 Critical Attributes

`.shape`: A tuple describing the dimensions. Your #1 debugging tool

- 90% of your errors in PyTorch will be shape mismatches

`.device`: Where the tensor lives.

- CPU or cuda (CPU)

`dtype`: The data type of the numbers. The default is `float32`.

###### Why Default float32?

`Tiny, continuous adjustent` to a model's weights is the entire engine of deep learning.

You can not nudge a parameter from `3` to `3.001` if your data type only allows whole numbers.

Thus, model parameters (weights, biases) **MUST** be a float type.

#### Data vs. Parameter

PyTorch: [AutoGrad](https://docs.pytorch.org/tutorials/beginner/blitz/autograd_tutorial.html)

The difference between `data` and `parameter` is **requires_grads** attribute in a tensor.

By default, a tensor is just data. To tell PyTorch it's a learnable parameter, we must set `requires_grads` to activate**AutoGrad**, which stands for `automatic differentiation`.

```python
# A standard data tensor
x_date = torch.tensor([[1., 2.], [3., 4.]])

# A parameter tensor (we need gradients)
w = torch.tensor([[1.0], [2.0]], requires_grad=True)

print(f"Data tensor requires_grad: {x_date.requires_grad}")
print(f"Parameter tensor requires_grad: {w.requires_grad}")
```

Results:

> Data tensor requires_grad: False
> Parameter tensor requires_grad: True

## Computation Graph

#### Building the Graph

In the last chapter, we set `requires_grad` to True. By setting up this attribute, PyTorch becomes able to build a **Computational Graph**.

The graph functions like a `live recording` of your operations.

Let build this graph in a simple example:

###### Goal: Compute z

Given `z = x * y`, and `y = a + b`, and `a = 2.0`, `b = 3.0`, `x = 4.0`, Let's using PyTorch to calculate the value of z.

To achieve this goal, firstly, we need to have our parameters.

```python
# Three parameter tensors, not data tensors
a = torch.tensor(2.0, requires_grad=True)
b = torch.tensor(3.0, requires_grad=True)
x = torch.tensor(4.0, requires_grad=True)
```

Then, by add `a` to `b`, we get our first result tensor, `y`. Later on, `z` is calculated by multiplying `x` and `y`:

```python
# First Operation
y = a + b

# Second Operation
z = y * x
```

Finally, the results `z` is printed out:

```python
print(f"Result z: {z}")
```

Results:

> Result z: 20.0

#### Examination of the Graph

PyTorch will automatically track the operations and build computation graph.

A **special attribute**,`.grad_fn`, can be found in tensors that is created by operation. And `.grad_fn` points out the operations that create it.

######

To prove this, let us check the tensors we have already made:

###### Tensor Created by User

```python
# z was created by multiplication
print(f"grad_fn for z: {z.grad_fn}")

# y was created by addition
print(f"grad_fn for y: {y.grad_fn}")
```

> grad_fn for z: <MulBackward0 object at 0x11324c4f0>
> grad_fn for y: <AddBackward0 object at 0x11324c4f0>

###### Tensor Created by Operation

```python
# a, b, x were created by the user, so they don't have a grad_fn
print(f"grad_fn for a: {a.grad_fn}")
print(f"grad_fn for b: {b.grad_fn}")
print(f"grad_fn for x: {x.grad_fn}")
```

> grad_fn for a: None
> grad_fn for b: None
> grad_fn for x: None

#### Roles of Graph

`grad_fn` we discussed before is the **tangible evidence** of the computation graph.

This tracing attributes plays a key role in PyTorch. When we call `loss_backword` in the future sections, PyTorch will walk the exact trail of breadrumbs to calculate the gradients for us.

In the previous section, we can see `z` points at the multiply operation and `y` points at the add operation. This is the perfect **map** of our calculations.

## Element-wise vs. Matrix Multiplication

#### Review of Previous Sections

In previous sections, we have

- `Tensor` -> the noun
- `AutoGrad` -> the nervous system

Now, we need the **verb** to train our models, which is `operation`.

The good news is that the vast majority of deep learning is just a few simple operations, repeated over and over.

Only a small number of operations (operators) we need to master.

#### Star Operator (\*): Element-wise

This operator is straight-forward, and only multiplies matching positions.

```python
a = torch.tensor([[1, 2], [3, 4]])
b = torch.tensor([[10, 20], [30, 40]])

# This calculates: [[1*10, 2*20], [3*30, 4*40]]
elementwise_product = a * b
print(f"Elementwise product:\n{elementwise_product}\n")
```

Results:

> Elementwise product:
> tensor([[10, 40],

        [ 90, 160]])

#### At Operator (@): Matrix Multiplication

This is the operator that powers neual networks.

When you build a linear layer: `y = Xw + b`. `@` operator is always referred tool.

```python
# shape: (2, 3)
m1 = torch.tensor([[1, 2, 3], [4, 5, 6]])

# shape: (3, 2)
m2 = torch.tensor([[7, 8], [9, 10], [11, 12]])

# Resulting shape will be (2, 2)
matrix_product = m1 @ m2
print(f"Matrix product:\n{matrix_product}\n")
```

> tensor([[10, 40],

        [ 90, 160]])

> Matrix product:
> tensor([[58, 64],

        [139, 154]])

## Reduction Operation & The dim Argument

A `reduction` is any operation that reduces a tensor to a smaller number of elements.

Things like `sum()`, `mean()`, and `max()`.

#### Default Behavior of Reduction

In default, reduction will always collapse the entire tensor:

```python
import torch

scores = torch.tensor([[10., 20., 30.], [5., 10., 15.]])

# This calculate: (10 + 20 + 30 + 5 + 10 + 15) / 6
average_scores = scores.mean()

print(f"Overall Mean: {average_scores}")
```

> Overall Mean: 15.0

#### Dim Argument in Reduction

In contrast of collapsing the entire tensor, the `dim` argument lets you control **which** direction to collapse.

The use of `dim` argument is **non-negotiable**, because it will be used everywhere.

###### Set-up:

In this example, our `score` tensor contains 2 students and 3 assignments.

| Score         | Assignment 1 | Assignment 2 | Assignment 3 | `mean(dim=1)` |
| ------------- | ------------ | ------------ | ------------ | ------------- |
| Student 1     | 10           | 20           | 30           | 20            |
| Student 2     | 5            | 10           | 15           | 10            |
| `mean(dim=0)` | 7.5          | 15           | 22.5         |               |

###### Reduction using `dim` Argument

`dim=0` collapses the rows, it operates "vertically".

`dim=1` collapses the columns, it operates "horizontally".

# Transformer

## Introduction

GPT-2: [Code for the paper "Language Models are Unsupervised Multitask Learners"](https://github.com/openai/gpt-2)

OpenAI Blog: [Better Language Models and Their Implications](https://openai.com/index/better-language-models/)

ChatGPT has been extremely popular in recent years.

However, the heart of GPT model is straightforward and can be summarized in the following 100 lines of Python code, as shown in the following sections.

###### The Roadmap of GPT-2 Model

1. Tokenized Text
2. GPT-2 Model
   - Token Embedding (tokens -> vectors)
   - Positional Embedding
   - Transformer Block (core engine)
     - Multi-HeadAttention
     - LaverNormalization
     - Feed ForwardNN
3. Output Layer (make the prediction)
4. Output Logits (B. T. vocab size)

## The GPT Config

#### Blueprint of Our GPT Model

The configuration of GPT model is wrapped into a dataclass as follows:

```python
@dataclass
class GPTConfig:
	vocab_size: int
	block_size: int				# max sequence length (context window)
	n_layer: int = 12			# Number of Transformer Blocks to stack
	n_head: int = 12			# Number of attention "heads"
	n_embd: int = 768			# The dimensionality of our vectors
	dropout: float = 0.1
```

This is awesome, because by just changing the numbers in `GPTConfig`, we can switch from a **toy** model to the **full-scale** GPT-2.

#### Real GPT-2 Configs

| Parameter    | What it Controls    | Intuition                                                 | Real GPT-2 (Small) |
| ------------ | ------------------- | --------------------------------------------------------- | ------------------ |
| `vocab_size` | Vocabulary Size     | How many **unique words** the model knows                 | 50257              |
| `block_size` | Context Window      | How far back the model can "see" at once                  | 1024               |
| `n_layer`    | Model **Depth**     | How many `Blocks` are stacked. More layer = more powerful | 12                 |
| `n_head`     | Model **Width**     | How many parallel "conversations" attention can have      | 12                 |
| `n_embd`     | Embedding Dimension | The "size" of the vectors representing each tokens        | 768                |

## Token Embeddings

#### Problems We are Solving

The Problem: **RAW TOKEN IDS**

The **input** to our model is a sequence of numbes, like [5, 21, 108]. But these are just meaningless IDs from a vocabulary list.

- The distance between IDs are meaningless
  - e.g. The number `21` is NOT 5 times than number `5` in token IDs
  - Thus, neural network can not do math on IDs
- The location (distance) of our inputs should mean something
  - A good way to achieve this is vectorization

#### Transforming Token to Vectors

Pytorch: [Tensor](https://docs.pytorch.org/docs/stable/tensors.html)

We would like to have a representation where words with similar meanings will end up close to each other in a high-dimensional space.

Thus, we initiate `nn.Embedding` instance to do that, it will return a `tensor` object after finishing.

###### Transformer's Solution

The mechanism we solve this problem is `nn.Embedding` Layer.

```python
import torch
import torch.nn as nn

# A ting config for our example
vocab_size = 10
n_embd = 3      # The number of dimensions in our "semantic space"

# The layer is our coordinate book
token_embedding_tables = nn.Embedding(num_embeddings=vocab_size,
                                      embedding_dim=n_embd)

# The book itself is the .weight attributes. Each row is a word's coordinate.
print(f"Shape of our coordinate book: {token_embedding_tables.weight.shape}")
print("Content of the book (initially random coordinates book):")
print(token_embedding_tables.weight)
```

###### Review of Its Content

`require_grad` is very important in this tensor.

During training, our model will **learn** the best possible coordinates for each word. To help it make better predictions.

> Shape of our coordinate book: torch.Size([10, 3])
> Content of the book (initially random coordinates):
> Parameter containing:
> tensor([[-0.6162, 0.3905, 0.6532], #Coordinate for token 0

        [-0.3948,  0.8454, -1.6533],		#Coordinate for token 1
        [-0.3523,  1.8943, -0.0944],		#Coordinate for token 2
        ...
        [-0.3326, -0.0927, -0.2539]], requires_grad=True)

## Posititional Embeddings

#### The Problem of Word Embedding

Traditional word embedding algorithms can achieve the following:

> Vector_king - vector_man + vector \_woman ≈ vector_queen

However, it has a huge flaw: **Static** and **Context-Free**

For example, the model can not understand the meaning of `bank` if the vector is **identical** in these sentences

> I sat on the river bank.
>
> I withdrew money from the bank.

###### Positional Embedding in Transformer

Based on its context, transformer can dynamically adjust token's vector

To achieve this goal, we should give our model a sense of **order**.

In transformer, instead of learning a unique vector for each **word**, we will learn a unique vector for each **position**

It requires another `nn.Embedding` layer, which give each position a vector.

e.g. The word `the` in position 5 do NOT equal `the` in position 20

#### Combine Token Embedding and Positional Embedding

####

## Self-Attention Intuition

`Self-Attention` allows every word to dynamically pull in information from its context to refine its own meaning.

This is the formula:

$$
\mathrm{Attention}(Q, K, V) = \mathrm{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

- Query (Q): The word's `search query`, what it is looking for,
- Key (K): The word's `label`, what it **is**
- Value (V): The word's `payload`, the information it offers.

#### Example: Crane

In the following sentences, `crane` have two distinct meanings.

The **Ambiguity** of crane's meaning can be solved by **listening to its neighbors**.

> 1. "The crane ate a fish." (crane = a bird)
> 2. "The crane lifted the steel." (crane = a machine)

###### Starting Point

To make it simple, we will adopt a 2D space:

> Dimension 1: Represents "Is it an Animal"?
>
> Dimension 2: Represents "Is it a Machine"?

At the very beginning, the starting vectors for `crane` is **identical** in both sentences.

The meaning of `crane` is ambiguous, so we represent it using `[0.5, 0.5]`.

| Token  | Q - "I'm looking for ..." | K - "I am ..."            | V - "I offer this info ..." |
| ------ | ------------------------- | ------------------------- | --------------------------- |
| crane  | [0.7, 0.7]                | [0.7, 0.7]                | [0.5, 0.5] (Ambiguous)      |
| ate    | ...                       | [0.9, 0.1] (High Animal)  | [0.9, 0.1]                  |
| fish   | ...                       | [0.8, 0.2] (High Animal)  | [0.8, 0.2]                  |
| lifted | ...                       | [0.1, 0.9] (High Machine) | [0.1, 0.9]                  |
| steel  | ...                       | [0.2, 0.8] (High Machine) | [0.2, 0.8]                  |

###### Updating Vectors

We need a mechanism to **UPDATE** this vector based on its neighbors. This mechanism is called **Self-Attention**.

Self-Attention are achieved in three steps, as follows

1. Scoring
2. Normalizing (softmax): score to percentage
3. Aggregation: Weighted sum of value vectors

###### Sentence 1

###### Sentence 2

PyTorch: [Softmax](https://docs.pytorch.org/docs/stable/generated/torch.nn.Softmax.html)

`Softmax` rescales Tensor so that the elements of the n-dimensional output Tensor lie in the range [0, 1] and sum to 1.

> Before softmax:
>
> [2.0, 1.0, 0.1, -0.5]
>
> After softmax:
>
> [0.60, 0.22, 0.09, 0.05]

###### Reference

[PyTorch in 1 Hour](https://www.youtube.com/watch?v=r1bquDz5GGA&t=57s)

[Give me 100 min, I will make Transformer click forever](https://www.youtube.com/watch?v=CfJ3Cxtlcps&t=4094s)
