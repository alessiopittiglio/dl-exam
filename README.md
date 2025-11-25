# Sentence Reconstruction
The goal of the project is to build a neural network capable of taking a random permutation of words as input and reconstructing the original English sentence.

## Constraints
The project was subject to a set of constraints:
- No pre-trained models
- The model had to be lightweight (<20M parameters)
- No post-processing
- No external data

## Dataset and Preprocessing

The dataset is composed of sentences taken from the `generics_kb` dataset available on Hugging Face. We restricted the vocabulary to the 10,000 most frequent words and retained only sentences making use of this vocabulary and with a length greater than 8 words. Data augmentation was applied by generating training pairs in which the target remained unchanged, while the input sequence was created by randomly shuffling its words.

## Methodology
The proposed solution implements a sequence-to-sequence Transformer developed from scratch using TensorFlow/Keras.

## Metrics
The quality of the reconstruction is evaluated using a custom metric based on the Longest Common Substring (LCS):

$$
\text{Score} = \frac{|w|}{\max(|s|, |p|)}
$$

where $w$ is the longest common substring between the prediction $p$ and the source $s$. A score of 1.0 indicates a perfect match.

## Results

### Quantitative Results
After training, the model achieved an average score of 0.4423 on a random sample of 3,000 test sentences.

### Qualitative Results
Below, we present some examples:

| Type | Sentence |
| :--- | :--- |
| **Original**          | `nuclear power is in decline in the united states` |
| **Input (Shuffled)** | `united nuclear in in power the states decline is` |
| **Prediction**        | `nuclear power is in decline in the united states` |

| Type | Sentence |
| :--- | :--- |
| **Original** | `advertising is most prominent in a free market economy` |
| **Input (Shuffled)** | `in market prominent a economy is free advertising most` |
| **Prediction** | `advertising is most prominent in a free market economy` |
