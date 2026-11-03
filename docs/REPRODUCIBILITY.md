# Reproducibility and experimental setup

## Tasks and datasets

The project used three course-provided HDF5 datasets:

| Part | Dataset | Task |
| --- | --- | --- |
| 1 | glyph_80k.h5 | Single glyph classification |
| 2 | infix_88k.h5 | Stroke sequence to infix expression |
| 3 | postfix_208k.h5 | Stroke sequence to postfix expression |

The datasets are not included in this public repository.

## Shared settings

- Random seed: **2026**
- Batch size: **128**
- Final reported training runs: **CPU**
- Hardware used for the project: AMD Ryzen 5 5600, AMD Radeon RX 6600, 16 GB RAM, Windows 10
- Checkpoint selection: validation performance

## Part 1

- Optimiser: Adam
- Loss: cross entropy
- Learning rate: 1e-4
- Full run: 18 epochs
- Selected checkpoint: epoch 15

## Part 2

- Optimiser: AdamW
- Loss: cross entropy with padding ignored
- Learning rate: 1e-3
- Gradient clipping
- ReduceLROnPlateau scheduler
- Decaying teacher forcing
- Full run: 30 epochs
- Selected checkpoint: epoch 29

## Part 3

- Optimiser: AdamW
- Loss: cross entropy with padding ignored
- Learning rate: 1e-3
- Gradient clipping
- ReduceLROnPlateau scheduler
- Full run: 18 epochs
- Selected checkpoint: epoch 18

## Public-code limitation

The original project was completed inside UCD COMP47650 coursework scaffolding. The supplied source files and datasets include explicit restrictions against public redistribution. For that reason, this repository documents the work without republishing restricted starter code, datasets or checkpoints.
