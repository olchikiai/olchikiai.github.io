---
title: "Why Ol Chiki Needs a Morphological Analyzer"
date: 2026-04-09
draft: false
mermaid: true
math: true
description: "Why the Ol Chiki script requires a dedicated morphological analyzer, covering infixes, bound morphemes, and diacritic challenges for ML pipelines."
---

The Ol Chiki script requires a Morphological Analyzer, but it is crucial to separate the writing system (the visual script) from the language structure (the grammar).
Ol Chiki is the graphic alphabet used to write the Santali language. Because Santali is an agglutinative language, any system processing it—whether written in Ol Chiki, Devanagari, or the Latin script—must use a Morphological Analyzer to understand its meaning.
When building an NLP or AI architecture specifically for the Ol Chiki script, the Morphological Analyzer handles distinct layers of the pipeline.

---

### 1. The Processing Pipeline (Where the Analyzer Sits)
When a machine processes raw Ol Chiki text, it must go through an architecture where the Morphological Analyzer acts as the core interpreter:

```mermaid
flowchart TD
[ Printed/Handwritten Ol Chiki ]
               │
               ▼ (1. Vision Layer: OCR)
   [ Digital Ol Chiki Unicode ]  ──> e.g., ᱫᱟᱞᱮᱫᱠᱳᱣᱟ (daletkoa)
               │
               ▼ (2. Text Normalization / G2P)
   [ Standardized Script Array ]
               │
               ▼ (3. Linguistic Layer: MORPHOLOGICAL ANALYZER)
 [ ᱫᱟᱞ (dal / hit) ] + [ ᱮᱫ (et' / PresCont) ] + [ ᱠᱳ (ko / them) ] + [ ᱣᱟ (a / Finite) ]
               │
               ▼ (4. Downstream ML Model)
   [ Context Vector Embeddings / Translation / LLM Inference ]

```
---

### 2. Specific Challenges of Ol Chiki for ML Architects
While the underlying grammar requires morphological decomposition, the physical structure of the Ol Chiki script introduces unique challenges that make a dedicated analyzer even more critical:

### A. The Non-Linear Morphological Infix Challenge
Tokenizers typically scan text sequentially from left to right. However, Santali uses internal infixes to change word meanings (e.g., inserting ᱯ (-p-) inside ᱫᱟᱞ (dal) to make ᱫᱟᱯᱟᱞ (dapal - to fight each other)).

* A standard sequential BPE tokenizer sees ᱫᱟᱞ and ᱫᱟᱯᱟᱞ as entirely unrelated character strings.
* An Ol Chiki Morphological Analyzer uses structural rules to identify the infix character in the middle of a syllable, extract it, and map it to a "reciprocal action" feature tag.

### B. The Lack of Visual Word Boundaries for Bound Morphemes
In Indo-Aryan scripts (like Devanagari for Hindi), postpositions are often separated by spaces (e.g., घर में). In Ol Chiki, complex case suffixes are written as a single, continuous string attached to the noun (e.g., ᱳᱲᱟᱜᱨᱮᱠᱷᱳᱱᱟᱜ / oṛak'rekhonak').

* Without a Morphological Analyzer to slice these continuous character strings at the exact boundaries of the case suffixes (ᱨᱮ, ᱠᱷᱳᱱ, ᱟᱜ), your vocabulary size will grow exponentially, causing your model's embedding layer to run out of memory.

### C. Diacritics and Phonetic Modifiers (Muha Tudak)
Ol Chiki uses specific diacritic marks, like the Muha Tudak (a nasalisation dot) and the Ohcet (a glottal stop modifier). These modifiers alter the pronunciation and meaning of a root word.

* A Morphological Analyzer cleans up and normalizes these modified characters before feature extraction, ensuring that slight spelling variations of the same root word do not create separate, fractured vector representations in your model.


