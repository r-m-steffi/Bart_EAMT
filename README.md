
# Entity-Aware Machine Translation (SemEval 2025 Task 2)

This repository implements an Entity-Aware Machine Translation (EA-MT) system for SemEval 2025 Task 2. The system leverages the multilingual mBART-50 model, augmented with entity annotations, to improve translation quality across languages—specifically English to French.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Dataset](#dataset)
- [Installation](#installation)
- [Training](#training)
- [Evaluation](#evaluation)
- [Results](#results)
- [License](#license)

## Overview

This project explores how injecting entity information into source text can improve translation quality. We fine-tune the `facebook/mbart-large-50-many-to-many-mmt` model using entity-tagged training data from SemEval 2025 Task 2.

##  Features

-  Named Entity-aware translation
-  Tokenization with Hugging Face Datasets and Tokenizers
-  Fine-tuning mBART-50 on entity-rich parallel data
-  BLEU evaluation with sacrebleu
-  Before/after comparison with base model

## Dataset

- Format: JSONL with keys `source`, `target`, and `mention`
- `target` may contain multiple translations.
- Used custom flattening and tokenization pipelines
- Entity mentions wrapped in `<entity> ... </entity>`

## Installation

```bash
git clone https://github.com/r-m-steffi/Bart-EAMT.git
cd Bart-EAMT
pip install -r requirements.txt```

## Training Configuration

- Model: `facebook/mbart-large-50-many-to-many-mmt`
- Language pair: English (`en_XX`) → French (`fr_FR`)
- Batch size: 4
- Epochs: up to 10
- Learning rate: 1e-5
- Early stopping: patience 2
- Metric: SacreBLEU
- Eval strategy: Every epoch

## Evaluation

| Model        | BLEU Score |
|--------------|------------|
| Base mBART   | 19.90      |
| Fine-tuned   | 16.51      |

> Although the fine-tuned model currently underperforms, future improvements will focus on:
> - Better entity preprocessing
> - Learning rate tuning
> - Using multiple translations per source sentence

## License

NONE

## Acknowledgements
- Prof. Abbas Akkasi
- SemEval 2025 Task 2 Organizers
- Hugging Face Transformers & Datasets
- spaCy for NER tagging
- Google Colab for compute support
