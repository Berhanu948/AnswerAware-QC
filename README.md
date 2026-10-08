# Amharic Answer-Aware Medical Question Classification

This project focuses on **Amharic Answer-Aware Medical Question Classification**, a Natural Language Processing (NLP) task that classifies medical questions into predefined question types by considering both the question and its corresponding answer. The approach is designed for Amharic, a relatively low-resource language, and aims to support research in medical NLP, question classification, and medical education.

## Overview

Question classification is an important component of medical question-answering systems because identifying the type of a question can help determine the appropriate strategy for processing and answering it.

In this project, an **answer-aware classification approach** is investigated, where the model uses both the medical question and its corresponding answer as input. Unlike conventional question classification, which relies only on the question text, the answer-aware setting incorporates answer information to determine the question type.

The task can be formulated as:

$$
f(q,a) \rightarrow y
$$

where:

* \(q\) represents the Amharic medical question,
* \(a\) represents the corresponding answer,
* \(y\) represents the question category.

## Dataset

The project uses an Amharic medical question–answer dataset containing **2691 463manually curated question–answer pairs**.

Each instance consists of:

* **Question** – an Amharic medical question
* **Answer** – the corresponding medical answer
* **Category** – the question type

The dataset contains four question categories:
| Category    |     Count |  Percentage |
| ----------- | --------: | ----------: |
| Description |     1,132 |  **42.07%** |
| List        |       807 |  **29.99%** |
| Definition  |       463 |  **17.21%** |
| Factoid     |       289 |  **10.74%** |
| **Total**   | **2,691** | **100.00%** |




## Answer-Aware Classification

The main experimental setting uses the question and answer together as a unified input.

```text
Amharic Question
       +
Amharic Answer
       ↓
   Tokenization
       ↓
 Classification Model
       ↓
 Question Category
```

For example:

```text
Question: የደም ግፊት ምንድነው?
Answer: የደም ግፊት ደም በደም ሥሮች ግድግዳ ላይ የሚያሳድረው ግፊት ነው።
Category: Definition
```

The answer provides additional semantic information that may help distinguish between categories such as **Definition, Description, List, and Factoid**.

## Experimental Settings

Two complementary settings can be used to examine the contribution of answer information.

### Question Classification (QC)

Only the question is provided to the model:

<p align="center">
  <strong>f(q) → y</strong>
</p>

```text
Question → Model → Category
```

### Question–Answer Classification (QAC)

Both the question and answer are provided:

<p align="center">
  <strong>f(q, a) → y</strong>
</p>

```text
Question + Answer → Model → Category
```

Comparing these settings allows the contribution of answer information to be investigated directly.

## Classification Models

The project evaluates several neural and Transformer-based architectures, including:


* **LSTM**
* **BiLSTM**
* **GRU**
* **CNN**
* **mBERT**


The conventional deep-learning models provide baseline comparisons, while Transformer-based models are used to capture contextual relationships within Amharic medical text.

## Processing Pipeline

The overall workflow is:

```text
Amharic Medical QA Dataset
             ↓
      Data Preprocessing
             ↓
    Question + Answer Pair
             ↓
        Tokenization
             ↓
    Train/Validation/Test Split
             ↓
       Classification Model
             ↓
     Question Type Prediction
             ↓
          Evaluation
```

## Question Categories

### Factoid

Questions seeking a short and specific factual answer.

### List

Questions that require multiple items, examples, symptoms, causes, treatments, or related entities.

### Definition

Questions asking for the meaning or definition of a medical term or concept.

### Description

Questions requiring a more detailed explanation or description of a medical condition, process, or concept.

## Evaluation Metrics

The classification models are evaluated using standard metrics:

* Accuracy
* Precision
* Recall
* Macro-F1
* Weighted-F1
* Confusion Matrix
* Classification Report

**Macro-F1** is emphasized because the dataset contains an imbalanced distribution across the four categories.

## Data Preprocessing

The preprocessing pipeline includes:

* Missing-value checking
* Duplicate detection
* Text cleaning
* Unicode normalization
* Question–answer consistency checking
* Category validation
* Tokenization
* Input-length management

For Transformer models, the corresponding pretrained tokenizer is used. For LSTM, BiLSTM, GRU, and CNN models, the text is converted into numerical representations suitable for neural-network training.

## Dataset Format

The dataset is provided as a UTF-8 encoded CSV file.

```text
question,answer,category
```

Example:

```text
question,answer,category
"የደም ግፊት ምንድነው?","የደም ግፊት ደም በደም ሥሮች ግድግዳ ላይ የሚያሳድረው ግፊት ነው።","Definition"
```

## Repository Structure

```text
Amharic-Answer-Aware-Medical-Question-Classification/
│
├── data/
│   └── AmhMedQA.csv
│
├── preprocessing/
│   └── preprocessing.py
│
├── models/
│   ├── lstm.py
│   ├── bilstm.py
│   ├── gru.py
│   ├── cnn.py
│   ├── mbert.py
│   
│
├── evaluation/
│   ├── evaluation.py
│   ├── classification_report.py
│   └── confusion_matrix.py
│
├── results/
│   └── figures/
│
├── requirements.txt
└── README.md
```

## Applications

The proposed approach can support research and development in:

* Amharic medical NLP
* Medical question classification
* Answer-aware question classification
* Medical question-answering systems
* Medical education systems
* Low-resource language NLP
* Intelligent medical information systems
* Question routing and intent classification

## Future Work

Future work may investigate:

* Larger Amharic medical QA datasets
* Amharic-specific pretrained language models
* Multilingual Transformer models
* Retrieval-augmented question answering
* Answer-aware question generation
* Medical document retrieval
* Generative Amharic QA
* Explainable question classification
* Robustness and shortcut-ablation analysis

## Disclaimer

This project is intended for **research and educational purposes**. It should not be used as a substitute for professional medical advice, diagnosis, or treatment.

## License

The dataset is intended to be released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.

Users may share and adapt the dataset provided that appropriate attribution is given.

## Citation

If you use this dataset or the associated resources in your research, please cite the corresponding publication:

```bibtex
@article{amhmedqa,
  title={Amharic Medical Question Answering Dataset for Medical Education and Natural Language Processing},
  author={Desta, Berhanu Bogale and Asfaw, Tesfa Tegegne and Abate, Solomon Teferra and Gebremeskel, Gebeyehu Belay},
  year={2026}
}
```

