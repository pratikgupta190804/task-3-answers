# Task 3 - The National Anthem Test

Model Used: BPE(Byte Pair Encoding)

## Goal
Compare tokenization behavior for the first stanza of Jana Gana Mana in:
- English transliteration
- Devanagari

## Input Texts Used
- input_english_national_anthem.txt (First Stanza)
  जन गण मन अधिनायक जय हे भारत भाग्य विधाता पंजाब सिंधु
- input_devanagari_national_anthem.txt (First Stanza)
  Jana Gana Mana Adhinayaka Jaya He Bharata Bhagya Vidhata Punjab Sindhu

## Method
1. Train one shared BPE tokenizer on both files.
2. Encode both files with the same trained model.
3. Count total tokens per script.
4. Compute fertility as:

Fertility = total_tokens / total_words

## Model Setup
- Model type: BPE
- Vocab size: 300
- Output artifact: artifacts/task3_anthem_bpe

## Results (Placeholder Values - Update Later)

### 1. Token Counts
- English transliteration token count: 84
- Devanagari token count: 101

### 2. Word Counts
- English transliteration word count: 52
- Devanagari word count: 52

### 3. Fertility Scores
- English transliteration fertility: 84 / 52 = 1.615
- Devanagari fertility: 101 / 52 = 1.942

## Interpretation
The Devanagari version shows higher token count and fertility in this run. The most likely reasons are:

1. Script characteristics
Devanagari words are often represented as richer grapheme patterns, and a small BPE vocabulary may split these patterns more often than transliterated Latin text.

2. Vocabulary pressure in a shared model
A single vocab of size 300 must serve two scripts. That creates competition between English-character subwords and Devanagari subwords, which can increase fragmentation for one or both scripts.

3. Training data size and coverage
If the anthem text itself is short (and the full training corpus is limited), many meaningful chunks are not learned as stable merges. This increases token count, especially for less frequent script patterns.

4. Pre-tokenization and normalization effects
Whitespace boundaries, punctuation handling, and script-aware normalization can all alter how subwords are formed, which directly affects fertility.

## Bonus: External Tokenizer Comparison (Placeholder Values)
External tokenizer: tiktoken (cl100k_base)

- English transliteration tokens: 68
- Devanagari tokens: 124

Approx fertility (using same 52-word denominator):
- English transliteration: 68 / 52 = 1.308
- Devanagari: 124 / 52 = 2.385

## What This Difference Reveals
Compared with the project tokenizer, the external tokenizer appears:
- More efficient on English transliteration (lower fertility)
- Less efficient on Devanagari in this example (higher fertility)

This usually indicates that the external tokenizer vocabulary is more optimized for high-frequency web and English-centric patterns than for this specific Devanagari text. In contrast, a custom tokenizer trained with balanced Indic data can reduce Devanagari fragmentation.

## Final Conclusion (Draft)
In this experiment, Devanagari has higher fertility than English transliteration. The difference is driven by a combination of:
- script-level segmentation behavior,
- limited shared vocabulary size,
- and corpus coverage during training.

After replacing placeholder values with measured values, this report can be used as the final Task 3 submission.
