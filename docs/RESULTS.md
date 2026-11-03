# Results

## Final selected models

| Part | Model | Parameters | Selected epoch | Validation | Test |
| --- | --- | ---: | ---: | ---: | ---: |
| 1 | GlyphCNN | 46,738 | 15 | 90.3000% accuracy | **90.79% accuracy** |
| 2 | Recurrent infix model | 179,022 | 29 | 97.2893% LA, 2.9227% CER | **95.10% LA, 5.27% CER** |
| 3 | Postfix Transformer | 48,135 | 18 | 96.6885% LA, 2.9991% CER | **95.59% LA, 3.61% CER** |

## Part 1

The initial baseline was a flattened logistic regression classifier with 6,966 parameters. A reconstructed run achieved 6.81% test accuracy.

The final GlyphCNN used three 1D convolution blocks with batch normalisation, ReLU and max pooling. It achieved 90.79% test accuracy with 46,738 parameters.

This part showed the largest absolute improvement over the starter baseline, although it remained the weakest of the three final systems relative to the task benchmark.

## Part 2

The infix task required autoregressive sequence generation without attention.

An older recurrent baseline used approximately 295,138 parameters and achieved about 91.09% test Levenshtein Accuracy with 9.02% CER.

The final model reduced the parameter count to 179,022 while improving test performance to 95.10% LA and 5.27% CER.

The main changes were:

- smaller recurrent hidden dimensions
- improved masking
- AdamW instead of Adam
- gradient clipping
- validation-driven learning-rate reduction
- a decaying teacher forcing schedule

## Part 3

The postfix task used a manually implemented encoder-decoder Transformer.

The final configuration used:

- d_model = 32
- 4 attention heads
- feed-forward dimension = 64
- 2 encoder layers
- 2 decoder layers
- dropout = 0.1

It achieved the strongest overall sequence result: 95.59% test Levenshtein Accuracy and 3.61% forced CER with only 48,135 parameters.

## Main takeaway

The project provided a useful comparison between model families rather than a simple model-scaling exercise. The final Transformer delivered the best sequence quality with less than one third of the parameter count of the recurrent model.
