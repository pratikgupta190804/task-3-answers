# Task 3 — The National Anthem Test

Model Used: BPE(Byte Pair Encoder)

## Setup

### Inputs

### 1. English Transliteration

**File:** `input_english_national_anthem.txt`

```
Jana Gana Mana Adhinayaka Jaya He
Bharata Bhagya Vidhata
Punjab Sindhu Gujarat Maratha
Dravida Utkala Banga
Vindhya Himachala Yamuna Ganga
Ucchala Jaladhi Taranga
Tava Shubha Name Jage
Tava Shubha Ashisha Mage
Gahe Tava Jaya Gatha
Jana Gana Mangala Dayaka Jaya He
Bharata Bhagya Vidhata
Jaya He Jaya He Jaya He
Jaya Jaya Jaya Jaya He
```

---

### 2. Devanagari Script

**File:** `input_devanagari_national_anthem.txt`

```
जन गण मन अधिनायक जय हे
भारत भाग्य विधाता
पंजाब सिंधु गुजरात मराठा
द्राविड़ उत्कल बंग
विंध्य हिमाचल यमुना गंगा
उच्छल जलधि तरंग
तव शुभ नामे जागे
तव शुभ आशीष मागे
गाहे तव जय गाथा
जन गण मंगलदायक जय हे
भारत भाग्य विधाता
जय हे जय हे जय हे
जय जय जय जय हे
```

---

## Tokenizer Training

The tokenizer was trained using both scripts to simulate a **multilingual vocabulary**.

```bash
abctokz train \
  --corpus data/input_devanagari_national_anthem.txt data/input_english_national_anthem.txt \
  --model bpe \
  --vocab-size 300 \
  --output artifacts/task3_anthem_bpe
```

Training on both scripts ensures that the tokenizer learns **shared subword units across languages**, which allows us to compare tokenization behavior between Latin transliteration and Devanagari.

---

## Encoding

After training, each file was encoded using the trained tokenizer.

```bash
abctokz encode --model artifacts/task3_anthem_bpe --input data/input_english_national_anthem.txt
abctokz encode --model artifacts/task3_anthem_bpe --input data/input_devanagari_national_anthem.txt
```

Token counts and fertility metrics were then computed using the repository’s evaluation utilities.

---

## Metrics

The key metric used in this experiment is **Fertility**, defined as:

```
fertility = tokens / words
```

This metric indicates how many tokens are produced per word.
Higher fertility means **more token fragmentation**, indicating lower tokenization efficiency.

---

## Results

| Script                  | Tokens | Words | Fertility |
| ----------------------- | ------ | ----- | --------- |
| English Transliteration | TBD    | TBD   | TBD       |
| Devanagari              | TBD    | TBD   | TBD       |

---

## Goal of the Experiment

This experiment evaluates how a multilingual tokenizer handles:

* Latin transliteration vs. native script
* Vocabulary allocation across scripts
* Token fragmentation differences

The results help reveal **biases in tokenizer vocabulary and training data coverage**.

---

## Bonus Experiment

For comparison, the same text can also be encoded using the tokenizer used by modern large language models via the **`tiktoken`** library. This provides a reference point for how production tokenizers handle Indic scripts.
