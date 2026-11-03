# Handwritten Mathematical Expression Recognition

Deep learning project comparing convolutional, recurrent and Transformer architectures for **online handwritten mathematical expression recognition from stroke sequences**.

Completed for **COMP47650 Deep Learning** at University College Dublin.

## Overview

The project was split into three increasingly difficult tasks:

1. **Glyph classification**: classify a single handwritten symbol from stroke data.
2. **Infix recognition**: map variable-length stroke sequences to infix mathematical expressions.
3. **Postfix recognition**: map stroke sequences to postfix notation with an encoder-decoder Transformer.

The emphasis was on compact models, careful masking, validation-based checkpoint selection and direct comparison between different sequence modelling approaches.

## Results

| Part | Model | Parameters | Test result |
| --- | --- | ---: | ---: |
| 1 | 1D CNN glyph classifier | 46,738 | **90.79% accuracy** |
| 2 | CNN + manual recurrent encoder-decoder | 179,022 | **95.10% Levenshtein Accuracy**, 5.27% forced CER |
| 3 | Manual encoder-decoder Transformer | 48,135 | **95.59% Levenshtein Accuracy**, 3.61% forced CER |

The Transformer produced the strongest overall sequence result while using substantially fewer parameters than the recurrent model.

## Model design

### Part 1: GlyphCNN

A compact 1D CNN was used for 18-way glyph classification. The final network used three convolution blocks with batch normalisation, ReLU and max pooling, followed by a small fully connected head.

- Convolution channels: 16 → 32 → 64
- Hidden dimension: 32
- Dropout: 0.1
- Learning rate: 1e-4
- Selected checkpoint: epoch 15

### Part 2: Infix sequence model

The infix task used a CNN-based stroke encoder followed by a manually implemented bidirectional GRU-style encoder and autoregressive decoder.

The final version reduced model size relative to an earlier baseline and improved both validation and test sequence metrics.

- Stroke embedding: 64
- Encoder hidden size: 64
- Decoder hidden size: 96
- Token embedding: 48
- Dropout: 0.2
- Teacher forcing schedule: 1.00 → 0.10
- Learning rate: 1e-3
- Selected checkpoint: epoch 29

### Part 3: Postfix Transformer

The final system was a compact encoder-decoder Transformer implemented without high-level Transformer modules. It included manual multi-head attention, encoder and decoder blocks, sinusoidal positional encoding, padding masks and a causal decoder mask.

- Model dimension: 32
- Attention heads: 4
- Feed-forward dimension: 64
- Encoder layers: 2
- Decoder layers: 2
- Dropout: 0.1
- Learning rate: 1e-3
- Selected checkpoint: epoch 18

## Evaluation approach

Sequence models were evaluated using **Levenshtein Accuracy (LA)** and **forced Character Error Rate (CER)**. Checkpoints were selected using validation performance before final test evaluation.

Across the project, the main improvement did not come from increasing parameter count. The strongest sequence model was also the smaller of the two final sequence models.

## Reproducibility

The experiments used:

- Python and PyTorch
- Fixed random seed: 2026
- Batch size: 128
- Adam for Part 1
- AdamW, gradient clipping and ReduceLROnPlateau for Parts 2 and 3
- CPU training for the final reported runs

More detail is available in [docs/REPRODUCIBILITY.md](docs/REPRODUCIBILITY.md), with model-level results in [docs/RESULTS.md](docs/RESULTS.md).

## Repository scope

This repository is a **public project summary**. The COMP47650 starter files and course datasets contain explicit restrictions against public redistribution, so they are not reproduced here. Model checkpoints and course-provided data are also excluded.

The public documentation focuses on my model design, experimental choices, evaluation and final results.

## Tools

Python · PyTorch · NumPy · HDF5 · Matplotlib · editdistance

## Author

**James McClatchie**  
MSc Artificial Intelligence for Medicine and Medical Research  
University College Dublin
