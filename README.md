# Infix to Postfix Notation Translator

A Sequence-to-Sequence neural network built with TensorFlow/Keras to translate mathematical expressions.

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg) ![Language](https://img.shields.io/badge/Language-Python-blue.svg) ![Framework](https://img.shields.io/badge/Framework-TensorFlow-orange.svg)

---

### 📖 Table of Contents
* [About the Project](#-about-the-project)
* [✨ Features](#-features)
* [🧠 Model Architecture](#-model-architecture)
* [🚀 Getting Started](#-getting-started)
* [🔧 Usage](#-usage)
* [📊 Results](#-results)
* [📜 License](#-license)

---

## 📖 About the Project

This project implements a sequence-to-sequence (Seq2Seq) model to translate mathematical formulae from traditional **infix notation** to **postfix notation** (Reverse Polish Notation).

While infix notation (e.g., `a + b`) is human-readable, it can be ambiguous without strict rules for operator precedence and parentheses. Postfix notation (e.g., `a b +`) is unambiguous and perfectly suited for stack-based computer evaluation.

This model learns the grammatical rules of this translation task from a dataset of randomly generated, fully parenthesized expressions.

**Example:**
- **Infix Input:** `(a + (b * c))`
- **Postfix Output:** `a b c * +`

---

## ✨ Features

- **Infix to Postfix Translation**: Core functionality to translate symbolic expressions.
- **Encoder-Decoder Architecture**: Built with LSTM layers to handle sequence-to-sequence tasks.
- **Shared Embeddings**: Uses a single embedding layer for both encoder and decoder to improve efficiency and parameter sharing.
- **Handles Fully Parenthesized Expressions**: Trained specifically on expressions with a maximum syntactic depth of 3.
- **High Accuracy**: Achieves 100% prefix accuracy on the test dataset, demonstrating complete mastery of the task within the given constraints.

---

## 🧠 Model Architecture

The model is a standard **Encoder-Decoder** architecture ideal for sequence translation tasks.

1.  **Shared Embedding Layer**: Converts input tokens from both infix (encoder) and postfix (decoder) sequences into dense vectors. Using a shared layer is efficient as the vocabularies are nearly identical.

2.  **Encoder (LSTM)**: Processes the entire input infix sequence and compresses its semantic and syntactic information into a fixed-size **context vector** (the LSTM's final hidden and cell states).

3.  **Decoder (LSTM)**:
    - Is initialized with the context vector from the encoder.
    - Generates the output postfix sequence one token at a time.
    - In each step, it uses the previously generated token as input to predict the next, making the process **autoregressive**.

The process can be visualized as:
`Infix Sequence` ➡ `[Encoder (LSTM)]` ➡ `Context Vector` ➡ `[Decoder (LSTM)]` ➡ `Postfix Sequence`

---

## 🚀 Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

- Python 3.8+
- `pip` and `venv`

### Installation

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/FedericoMuccioli/neural-infix-to-postfix.git
    cd neural-infix-to-postfix
    ```

2.  **Create and activate a virtual environment:**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install the required packages:**
    ```sh
    pip install -r requirements.txt
    ```

---

## 🔧 Usage

Open and run the `Infix_to_postfix_notation.ipynb` notebook in a Jupyter environment.

You have two options for running the project:

### Train from Scratch
Simply run all the cells in the notebook from top to bottom. The "Model Training" section will train the network, which takes a few minutes on a GPU.

### Use Pre-trained Weights
1. Download the `infix_to_postfix.weights.h5` file from the **Releases** section of this repository.
2. Place the `.h5` file in the same root directory as the notebook.
3. The notebook will automatically detect and load these weights, allowing you to **skip the training cell** and proceed directly to evaluation.

---

## 📊 Results

The model was evaluated over 10 rounds on newly generated test sets, showing robust and perfect performance.

| Metric | Value |
| :--- | :--- |
| **Final Average Prefix Accuracy** | `1.0000` |
| **Standard Deviation** | `0.0000` |

The perfect score confirms that the model successfully learned the deterministic, rule-based task of translating infix expressions to postfix notation for the problem's constraints.

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.
