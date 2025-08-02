
# Entity-Aware Machine Translation (SemEval 2025 Task 2)

This repository implements an Entity-Aware Machine Translation (EA-MT) system for SemEval 2025 Task 2. The project evaluates two state-of-the-art translation models: mBART-50 and MarianMT, comparing their baseline and fine-tuned performances on entity-rich translation tasks across multiple language pairs.

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem)
- [Features](#features)
- [Dataset](#dataset)
- [Installation](#installation)
- [Training](#training)
- [Evaluation](#evaluation)
- [Results](#results)
- [License](#license)

## Overview

This project explores how injecting entity information into source text can improve translation quality across different neural machine translation architectures. We implement and compare two approaches:

mBART-50: Multilingual denoising pre-trained transformer fine-tuned on English→French translation
MarianMT: Opus-based neural machine translation model fine-tuned on English→German translation

Both models are augmented with entity annotations to assess their capability in handling named entities during translation.


Name Of Collaborators:
-  Shelly Tyagi
-  Steffi Michael


## Problem Statement


The task is to develop machine translation systems that can accurately translate named entities in input sentences across different language pairs:

Language Pairs:

English → German (mBART-50)
English → German (MarianMT)


Named entities include people, organizations, locations, dates, and other proper nouns
Named entities are often challenging for translation systems due to cultural, domain-specific, or contextual nuances
Accurate entity translation is critical for maintaining factual accuracy and preserving semantic meaning

##  Features
**Common Features**
Named Entity-aware translation with <entity> tag annotations
Custom tokenization and data preprocessing pipelines
Baseline vs fine-tuned model comparison
Comprehensive evaluation metrics
Entity mention coverage analysis

**mBART-50 Specific**
Multilingual capabilities leveraging facebook/mbart-large-50-many-to-many-mmt
BLEU and COMET evaluation with sacrebleu
Support for multiple target translations per source

**MarianMT Specific**

Specialized EN→DE translation using Helsinki-NLP/opus-mt-en-de
Entity-level performance metrics (precision, recall, F1, accuracy)
COMET score computation using pretrained metrics
Advanced mention coverage analysis

## Models
**mBART-50**

Base Model: facebook/mbart-large-50-many-to-many-mmt
Architecture: Multilingual denoising autoencoder
Language Pair: English (en_XX) → French (fr_FR)
Strengths: Robust multilingual representation, handles multiple language pairs

**MarianMT**

Base Model: Helsinki-NLP/opus-mt-en-de
Architecture: Transformer-based neural machine translation
Language Pair: English → German
Strengths: Optimized for specific language pairs, efficient inference

## Dataset

Format: JSONL with keys source, target/targets, and mention
Entity Annotation: Entities wrapped in <entity> ... </entity> tags
Multi-reference Support: Target field may contain multiple valid translations
Preprocessing: Custom flattening and tokenization pipelines for both models
Entity Types: People, organizations, locations, dates, and other named entities

## Installation

```bash
git clone https://github.com/r-m-steffi/Bart-EAMT.git
cd Bart-EAMT
pip install -r requirements.txt
```

## Training
**mBART-50 Configuration**

Model: facebook/mbart-large-50-many-to-many-mmt
Batch Size: 4
Epochs: Up to 10
Learning Rate: 1e-5
Early Stopping: Patience 2
Primary Metric: SacreBLEU
Evaluation Strategy: Every epoch

**MarianMT Configuration**

Model: Helsinki-NLP/opus-mt-en-de
Fine-tuning Strategy: Entity-aware training on EN→DE data
Evaluation Metrics: COMET, BLEU, Entity-specific metrics
Entity Preservation: Special handling for <entity> tags during training

## Evaluation
**mBart-50**
| Model        | BLEU Score |
|--------------|------------|
| Base mBART   | 19.90      |
| Fine-tuned   | 16.51      |

> Although the fine-tuned model currently underperforms, future improvements will focus on:
> - Better entity preprocessing
> - Learning rate tuning
> - Using multiple translations per source sentence

**MarianMT**
**| Model        | COMET Score | Entity Precision | Entity Recall | Entity F1 | Entity Coverage/accuracy |**

  | -------------|-------------|------------------|---------------|-----------|---------------------------|
  
  | Base MarianMT| 86.73       | 1.00             | 0.1950        | 0.3264    |     19.29%                | 
  
  | Fine-tuned   | 82.48       | 1.00             | 0.14          | 0.25      |       13.97%              |

## Evaluation Approach

**Standard Metrics:** BLEU, COMET scores for overall translation quality

**Entity-Specific Metrics:** Precision, recall, F1-score, and accuracy for named entity translation

**Mention Coverage:** Analysis of how well models preserve entity mentions

**Cross-Model Comparison:** Performance analysis across different architectures

## Future Work
**mBART-50 Improvements**

Enhanced entity preprocessing strategies
Learning rate optimization and hyperparameter tuning
Leveraging multiple translations per source sentence during training
Exploration of different entity tagging schemes

**MarianMT Enhancements**

Advanced entity-aware training techniques
Integration with multilingual entity linking
Cross-lingual entity consistency evaluation
Domain adaptation for specific entity types

**Combined Research Directions**

Cross-model ensemble approaches
Multi-language entity translation evaluation
Analysis of entity type-specific performance patterns
Integration of external knowledge bases for entity disambiguation

## License

NONE

## Acknowledgements
- Prof. Abbas Akkasi
- SemEval 2025 Task 2 Organizers
- Hugging Face Transformers & Datasets
- spaCy for NER tagging
- Google Colab for compute support
