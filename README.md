# Qwen Tokenizer Lite

[![PyPI version](https://badge.fury.io/py/q-tokenizer.svg)](https://pypi.org/project/q-tokenizer/)

A lightweight, standalone Python package for Qwen tokenization, extracted and optimized for simple installation via PyPI. It wraps `tiktoken` to provide fast encoding/decoding and includes utility functions for text processing.

## Installation

Install the package directly from PyPI:

```bash
pip install q-tokenizer
```

## Quick Start

The package initializes the tokenizer automatically using the bundled vocabulary file, so you can start tokenizing immediately.

```python
from q_tokenizer import count_tokens, has_chinese_chars, remove_chinese_chars

# 1. Count tokens easily
text = "Hello, this is a test string."
print(count_tokens(text)) 

# 2. Check for Chinese characters
print(has_chinese_chars("Hello World"))        # False
print(has_chinese_chars("Hello 世界"))         # True

# 3. Remove Chinese characters
clean_text = remove_chinese_chars("Hello 世界")
print(clean_text)  # Output: "Hello "
```

## Advanced Usage

For more control over the tokenization process, you can use the `QWenTokenizer` class directly.

### Initialization
The default vocabulary (`qwen.tiktoken`) is included in the package. If you have a custom vocabulary, you can pass the file path.

```python
from q_tokenizer import QWenTokenizer

# Initialize with default bundled vocab
tokenizer = QWenTokenizer()

# OR initialize with extra vocab
# tokenizer = QWenTokenizer(extra_vocab_file='path/to/extra_vocab.tiktoken')
```

### Encoding and Decoding

```python
text = "<|im_start|>user你好<|im_end|>"

# Tokenize
tokens = tokenizer.tokenize(text)
print(tokens)

# Encode to IDs
ids = tokenizer.encode(text)
print(ids)

# Decode back to string
decoded_text = tokenizer.decode(ids)
print(decoded_text)
```

### Truncation

Truncate text based on token count, useful for LLM context limits.

```python
long_text = """
A tokenizer whispers, each fragment to break,
From words into tokens, the journey begins.
Qwen counts the pieces, where meaning spin,
The rhythm of language yours, forever mine.
"""

# Standard truncation (keeps the start)
short_text = tokenizer.truncate(long_text, max_token=10)

# Smart truncation (keeps start and end, adds "..." in the middle)
smart_text = tokenizer.truncate(long_text, max_token=10, keep_both_sides=True)
```

## Features

*   **Plug & Play:** No need to manually download `qwen.tiktoken`; it is included in the package.
*   **Efficient:** Built on top of `tiktoken` for high performance.
*   **Special Tokens:** Full support for `<|im_start|>`, `<|im_end|>`, and other special tokens.
*   **Chinese Utilities:** Includes helper functions to detect and strip Chinese characters from text.


## License & Attribution

This project is licensed under the **Apache License, Version 2.0**. 

### Origin
The core tokenization logic in this package is derived from the [Qwen-Agent Repository](https://github.com/QwenLM/Qwen-Agent). 

### Why this exists
The original repository includes a wide range of dependencies. **q-tokenizer** was created for users who only need the essential tokenization functions without the overhead of the entire library. 

**Key modifications made to the original code:**
* **Modularized**: Extracted only the essential `QWenTokenizer` class and BPE logic.
* **Utility Additions**: Added standalone helper functions like `has_chinese_chars` and `remove_chinese_chars`.

---
