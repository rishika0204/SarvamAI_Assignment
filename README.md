# OCR and Ground Truth Text Alignment

## Overview
This repository provides methods for aligning OCR-generated texts with Ground Truth (GT) texts using deterministic and embedding-based alignment techniques. The primary goal is to evaluate different alignment methods by comparing OCR outputs with human-validated GT sentences.

## Contents
- **Deterministic Alignment**: Needleman-Wunsch algorithm based on edit distance (Levenshtein).
- **Embedding-based Alignments**:
  - **MiniLM multilingual model** (`paraphrase-multilingual-MiniLM-L12-v2`).
  - **indic-sentence-similarity-sbert** (`l3cube-pune/indic-sentence-similarity-sbert`).

## Installation

Install the required dependencies using:

```bash
pip install -qU sentence_transformers faiss-cpu jiwer rapidfuzz regex
```

## Data Preparation

The data structure should include two directories:

- `ocr/`: OCR outputs in JSON format.
- `gt/`: Ground truth texts in JSON format.

Example paths:
```
/content/ocr/**/*.json
/content/gt/**/*.json
```

## Methods Implemented

### 1. Deterministic Method
Uses dynamic programming with Levenshtein distance to align OCR and GT sentences.

### 2. Embedding-based Methods

#### MiniLM multilingual
Uses SentenceTransformer (`paraphrase-multilingual-MiniLM-L12-v2`) embeddings for reciprocal nearest neighbor alignment.

#### l3cube-pune/indic-sentence-similarity-sbert
Employs SentenceTransformer (`l3cube-pune/indic-sentence-similarity-sbert`) fine-tuned for Indic languages, along with FAISS indexing for efficient similarity search.

## Evaluation Metrics
Evaluations include:

- **Similarity (Levenshtein normalized)**
- **Word Error Rate (WER)**
- **Character Error Rate (CER)**

Evaluation provides mean and standard deviation of these metrics, along with percentage thresholds (≥0.50, ≥0.75, ≥0.95) for similarity scores.

## Usage
Run the alignment and evaluation scripts provided in the notebook:

```python
# Run deterministic alignment and evaluation
aligned_pairs_edit = align_edit(ocr_sentences, gt_sentences)

# Run embedding-based alignments
aligned_pairs_emb = embedding_based_alignment(ocr_sentences, gt_sentences, model_name)

# Evaluate methods
evaluate_and_summarize(aligned_pairs_edit, aligned_pairs_emb)
```

## Results
The evaluation will output detailed statistics comparing all alignment methods, such as similarity scores, WER, and CER distributions.

## Example Output
```
── Deterministic (edit-distance) ──  pairs: 12345
 similarity : 0.856 ± 0.107
 WER        : 0.123 ± 0.075
 CER        : 0.067 ± 0.039
 ≥0.50 sim :  95.5%
 ≥0.75 sim :  87.2%
 ≥0.95 sim :  42.9%
```

## Acknowledgments
- Sentence Transformers
- FAISS
- jiwer
- rapidfuzz



