# Byte-Pair-Encoding-for-Text-Tokenization
This project implements a Byte Pair Encoding (BPE) algorithm for text tokenization, training it on NLTK's Gutenberg Corpus and evaluating its accuracy, coverage, and F1-score against NLTK's standard punkt tokenizer.

# Solution Summary

- Implemented a **Byte Pair Encoding (BPE) algorithm** for text tokenization with a custom Python class `BPE`.

- **Core Components**:
  - `learner` function:
    - Iteratively identifies the most frequent character/subword pairs using `findMostFrequentPair`.
    - Merges selected pairs and updates `vocab` and `training_corpus`.
    - Repeats for a set `num_merges` (e.g., 1000).
  - `segmenter` function:
    - Breaks new text into characters.
    - Applies learned merge operations greedily in the order they were learned.
    - Outputs tokenized text based on trained vocabulary.

- **Experimental Setup**:
  - Trained BPE on NLTK Gutenberg books:
    - `austen-emma.txt`, `blake-poems.txt`, `shakespeare-hamlet.txt`.
  - Evaluated on:
    - `shakespeare-macbeth.txt`, `austen-persuasion.txt`, `whitman-leaves.txt`.
  - Reference tokenization:
    - NLTK’s `punkt` (`sent_tokenize` + `word_tokenize`).
  - Metrics:
    - Accuracy, coverage, precision, recall, F1-score, Jaccard similarity.

- **Key Insights**:
  - Produced **elbow plot** of "Vocab Length vs Frequency of Merges" (e.g., optimal ~200 merges for Blake corpus).
  - ROUGE F1-scores on test texts:
    - Austen (on Persuasion) → **0.04825**
    - Blake (on Whitman) → **0.02346**
    - Shakespeare (on Macbeth) → **0.06055**
  - Strengths:
    - Learns morphemes, frequent words/subwords.
    - Effectively handles **OOV words** by splitting into known subunits.
    - Language-independent.
  - Weaknesses:
    - Potential **loss of semantics** due to subword splitting.
    - Depends on predefined vocab size; risk of suboptimal splits or overfitting.
    - **Context-insensitive**; struggles with homographs.
  - Challenges:
    - **Slow processing** due to iterative merges; suggests potential improvements like parallelization.

- **Conclusion**:
  - Demonstrated hands-on implementation of BPE, quantitatively evaluated against standard tokenization.
  - Highlighted both capabilities and limitations, providing a solid foundation for further optimization.
