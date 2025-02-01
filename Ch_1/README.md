# 📚 Chapter 1: Introduction to Large Language Models  

Chapter 1 provides a concise yet insightful overview of **large language models (LLMs)** and their foundational concepts. It covers:  

- **Transformers, BERT, and GPT:**  
  Explains their key features, differences, and how they are interconnected.  

- **Architecture Diagrams:**  
  Includes clear and detailed diagrams illustrating the architectures of Transformer, BERT, and GPT models.  

- **Building an LLM:**  
  Offers an overview architectural diagram showcasing the various components involved in building a large language model, setting the stage for the topics explored throughout the book.  

This chapter serves as a comprehensive introduction, ensuring readers gain a strong foundational understanding before diving deeper.  




# Interview Concepts: BERT, GPT, and Transformers

Answers to common interview questions about **BERT**, **GPT**, and **Transformers**. 

---

## 1. Transformer Architecture

### Self-Attention Mechanism
- **What is self-attention, and how does it work?**
  - Self-attention allows a model to weigh the importance of different words in a sequence **relative to each other**.
  - It computes a weighted sum of the embeddings of all words in the sequence, where the weights are determined by the similarity between the word and every other word.

- **How does self-attention differ from traditional attention mechanisms?**
  - Traditional attention mechanisms compute attention between **two different sequences** (e.g., encoder and decoder).
  - Self-attention computes attention **within the same sequence**, capturing dependencies between all words.

- **What are queries (Q), keys (K), and values (V)?**
  - These are learned linear transformations of the input embeddings.
  - **Q**: Represents the word we are focusing on.
  - **K**: Represents the words we are comparing against.
  - **V**: Represents the information we aggregate based on the attention scores.

- **How is the attention score calculated?**
  - The attention score is calculated using the **scaled dot-product**:
    \[
    \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V
    \]

- **Why is scaling used in dot-product attention?**
  - Scaling by \( \sqrt{d_k} \) prevents the dot products from becoming too large, which can lead to small gradients during training.

---

### Multi-Head Attention
- **What is multi-head attention, and why is it used?**
  - Multi-head attention splits the input into multiple "heads," each computing self-attention independently.
  - This allows the model to focus on different parts of the sequence simultaneously, capturing diverse relationships.

---

### Positional Encoding
- **Why do Transformers need positional encoding?**
  - Transformers lack recurrence or convolution, so they have no inherent notion of word order.
  - Positional encoding adds information about the position of each word in the sequence.
  - Without positional encoding, the model would treat the input sequence as a bag of words, losing all information about the order of tokens. Example: The sentences "The cat chased the dog" and "The dog chased the cat" would be treated identically without positional information.
   - Self-Attention is Permutation-Invariant (means that shuffling the tokens in a sequence would produce the same attention scores).

- **How is positional encoding added?**
  - It is added to the input embeddings using sine and cosine functions of different frequencies:
    \[
    PE_{(pos, 2i)} = \sin\left(\frac{pos}{10000^{2i/d}}\right), \quad PE_{(pos, 2i+1)} = \cos\left(\frac{pos}{10000^{2i/d}}\right)
    \]

---

### Layer Normalization and Residual Connections
- **What is the role of layer normalization?**
  - It stabilizes training by normalizing the inputs across the features dimension.

- **Why are residual connections (a.k.a skip connections) important?**
  - These are are shortcuts that bypass one or more layers in a neural network. They help mitigate the vanishing gradient problem and enable training of very deep networks.

---

## 2. BERT (Bidirectional Encoder Representations from Transformers)

### Key Features
- **Why is BERT bidirectional?**
  - BERT uses bidirectional context (both left and right) to understand the meaning of a word, unlike GPT, which is unidirectional.

- **What is the difference between pre-training and fine-tuning?**
  - Pre-training trains the model on a large corpus (e.g., Masked Language Modeling).
  - Fine-tuning adapts the model to a specific task (e.g., sentiment analysis).

---

### Pre-Training Tasks
- **Masked Language Modeling (MLM):**
  - Randomly masks 15% of the tokens and predicts them using context from both directions.

- **Next Sentence Prediction (NSP):**
  - Predicts whether two sentences appear consecutively in the text.

---

### Tokenization
- **What is WordPiece tokenization?**
  - It splits words into subword units (e.g., "playing" → "play" + "##ing"), reducing the vocabulary size and handling OOV words.

---

## 3. GPT (Generative Pre-trained Transformer)

### Key Features
- **How does GPT differ from BERT?**
  - GPT is unidirectional (left-to-right) and uses causal language modeling for pre-training.

- **What is the pre-training objective?**
  - Predict the next word in a sequence, given all previous words.

---

### Fine-Tuning
- **How is GPT fine-tuned?**
  - Fine-tuning involves training on task-specific data (e.g., text classification) using supervised learning.

---

## 4