#### 13. Tokenizing Characters vs. Subwords vs. Words

###### Learning Objectives

1. The advantages and disadvantages of different "units" for vocab-creation and tokenization
2. Why should subword-based tokenization is the current best approach

###### What Is Token?

**Token** is a piece of text that can be represented as an integer, the corresponding number is called `token ID` or `token index`.

Example: `Hello`

- Character Level: `H`, `e`, `l`, `l`, `o`; 39, 68, 75, 75, 78
- Subword Level: `He`, `llo`: 1544, 18978
- Word: `Hello`: 15496

###### Pros and Cons of Tokenization Approaches

Current best tokenizers use a combination of characters, subwords, and words.

|                  | Character | Subword    | Word       |
| ---------------- | --------- | ---------- | ---------- |
| Sequence Length  | Long      | Variable   | Short      |
| Vocab Size       | Small     | Medium     | Very Large |
| OOV Handling     | Yes       | Mostly Yes | No         |
| Semantic Meaning | No        | Somewhat   | Yes        |
| Training Demands | Excessive | Low/Medium | Low        |

#### 14. Byte-pair Encoding Algorithm

###### Learning Objective

1. The mechanism of the BPE algorithm, which is widely used in real-world applications
2. How the BPE algorithm (simplified version) is implemented in Python
3. Additional steps used in professional tokenizers

###### BPE: Motivation and Theory

Tokenzation efficiency can be **improved** with tokens that represent longer character sequence (e.g. `the` instead of the [`t`, `h`, `e`])

###### BPE Algorithm

- Step 0: Initialize a vocabulary comprising only characters (no pairs)
- Step 1: Loop through the text and count the frequency of sequential pairs
- Step 2: Find the most frequent pair and merge them to create a new token
- Step 3: Add that new token to the vocabulary
- Step 4: Loop through the text and replace the sequence with that new pair

- Step 5: Repeat Step 1-4 until the vocab contains `k` tokens

###### Additional Steps to Create Professional Tokenizers

- Data Selection
- Cleaning and preprocessing (removing non-ASCII characters, excessive whitespace, formatting)
- Subword initialization ("ing", "er", "ly") or constrains (e.g., code, url, numbers)
- Experimenting with vocab size
- Merge based on bytes not charaters (for non-latin languages)
- Handling rare words to reduce OOV problems
- Post-training adjustments (removing or adding merges)
- Add special tokens
- Coding tricks to decrease compute time
