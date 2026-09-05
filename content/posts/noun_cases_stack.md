---
title: "Noun Case Stacking and Negation in Santali"
date: 2026-03-21
draft: false
math: true
---

### 1. How Noun Cases Stack (Agglutination in Nouns)
In Indo-Aryan languages like Hindi or Bengali, noun cases (prepositions/postpositions) are often written as separate words (e.g., ghar mein / "in the house"). In Santali, these cases are suffixes glued directly onto the noun.
If multiple relationships exist, the markers stack sequentially onto the base root without changing the root's shape.

### Case Suffix Tokens

* Base Noun: oṛak' (house)
* Locative Case Marker ("in / at"): -re
* Ablative Case Marker ("from"): -khon
* Possessive Case Marker ("of"): -ak'

### The Stacking Chain
Watch how individual grammatical instructions append to the end of the base noun:

   1. The Base:
   
   oṛak' → "house"
   
   2. Adding Location (-re):
   
   oṛak' + re = oṛak're → "in the house"
   
   3. Adding Direction/Source (-khon):
   
   oṛak' + re + khon = oṛak'rekhon → "from inside the house"
   
   4. Adding Possession (-ak'):
   
   oṛak' + re + khon + ak' = oṛak'rekhonak' → "that which belongs to the inside of the house"
   
   
---

### 2. How Negation Alters the Verb Chain
In inflectional languages, making a sentence negative usually means adding a word like "not" or "nahin" next to the verb. In Santali, negation structurally transforms the verb complex.
The negative marker bañ / ba- behaves like a prefix or an independent operator that dynamically pulls the subject and object markers away from the verb and attaches them to itself.

### Positive Sentence Structure

Amem ñeletkoa.


* Breakdown: Am (You) + -em (subject marker attached to pronoun) + ñel-et'-ko-a (see-present-them-finite).
* Meaning: "You are seeing them."

### Negative Sentence Structure (Using ba-)

When you introduce the negative particle ba-, the subject marker -em detaches from the pronoun and migrates over to the negative particle. The verb root drops its tense markers entirely because the negative state changes the syntax:

Am bam ñelko-a.


* Breakdown: Am (You) + ba- (not) + -m (moved subject marker) + ñel (see) + -ko (them) + -a (finite).
* Meaning: "You do not see them."

---

### The ML Architecture View: Canonical Parsing
For an ML architect designing tokenization or parsing strategies for Austroasiatic languages, these features require a Finite State Transducer (FST) or a specialized sub-word tokenizer rather than standard frequency-based BPE (Byte-Pair Encoding).
A canonical processing pipeline must map the stacked tokens deterministically:

[ Input String: oṛak'rekhonak' ] 
               │
               ▼ (Morphological Parser / FST)
 [ Root: oṛak' ] + [ Case1: Locative ] + [ Case2: Ablative ] + [ Case3: Possessive ]

This clean semantic decomposition is only possible because agglutinative boundaries do not distort or blend the adjacent character boundaries.

