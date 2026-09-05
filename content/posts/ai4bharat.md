---
title: "AI4Bharat and the Gaps in Santali Language AI"
date: 2026-08-11
draft: false
math: true
description: "An analysis of the technical gaps in AI4Bharat models like IndicTrans2 and IndicConformer when applied to the Santali language and Ol Chiki script."
---

While [AI4Bharat](https://ai4bharat.iitm.ac.in/) has achieved breakthroughs in digital accessibility for the Santali language, notable technical gaps persist when deploying models like [IndicTrans2](https://ai4bharat.iitm.ac.in/areas/model/NMT/IndicTrans2/) or [IndicConformer](https://github.com/AI4Bharat/IndicConformerASR) in production environments. [1, 2] 
These processing limitations span textual translation and audio engineering categories:
### 1. Translation & Textual Gaps (IndicTrans2)

- The Syntax Asymmetry Gap: While IndicTrans2 applies rule-based script unification to fold multiple languages into Devanagari to boost cross-lingual learning, Ol Chiki is kept isolated. Because Santali belongs to the Austroasiatic Munda family rather than the Indo-Aryan or Dravidian family, it misses out on structural transfer learning benefits from larger Indian language corpora. [3, 4, 5]
- Severe Asymmetry in Translation Direction: Benchmark studies reveal a deep performance gap based on vector direction. While translating Santali → English performs adequately (around 26.8 BLEU points on the [IN22 evaluation dataset](https://github.com/ai4bharat/IndicTrans2)), translating English → Santali (Ol Chiki) drops drastically to a low 7.3 BLEU points due to the model struggling with complex Santali word compounding and agglutination. [3]
- Noisy Training Data Artifacts: Large open-source datasets (such as NLLB datasets processed through automated semantic tools like LASER3) are heavily degraded for Santali. Human spot-checks reveal that a vast majority of parallel web data pairs contain mistranslations, meaning the model occasionally memorizes faulty grammatical syntax. [1]
- Named Entity & Token Corruption: Raw technical alphanumeric patterns—like URLs, formatting dates, or English abbreviations like "ID"—regularly get corrupted during translation into Ol Chiki script strings, requiring heavy external wrapper software pipelines like the IndicTransToolkit to resolve. [6, 7]

### 2. Audio & Speech Gaps (IndicConformer)

- High Real-World Word Error Rates (WER): While IndicConformer registers low Word Error Rates on curated reading datasets, its accuracy degrades dramatically when exposed to real-world conversational scenarios, shifting regional dialects, or background street noise. Emerging next-generation models (such as SraVaani 1.0) outperform it by up to 2–4% on diverse conversational tribal speech data benchmarks.
- Dialect and Script Friction: Santali audio datasets are frequently crowdsourced or transcribed by speakers who originally learned the language via alternative scripts (Bengali, Devanagari, or Latin). Acoustic alignments often mismatch when a speaker uses a regional dialect vocabulary variant that lacks an unambiguous phonetic representation in the static tokenizer map of the model.
- Telephony Downsampling: Standard models are optimized for crisp 16kHz audio inputs. When processing lower-quality 8kHz cellular phone audio data—such as public voice applications or support hotlines used in rural districts—acoustic frames regularly drop out, causing misrecognition of critical vowel modifiers. [8, 9, 10, 11, 12]


[1] [https://arxiv.org](https://arxiv.org/pdf/2305.16307)
[2] [https://github.com](https://github.com/AI4Bharat/IndicConformerASR)
[3] [https://www.techrxiv.org](https://www.techrxiv.org/doi/pdf/10.36227/techrxiv.176739490.05917259)
[4] https://models.ai4bharat.org
[5] [https://www.scribd.com](https://www.scribd.com/document/880627420/LLM-AI4Bharath)
[6] [https://www.anuvad.ai](https://www.anuvad.ai/blog/ai4bharat-indictrans-preprocessing)
[7] [https://www.anuvad.ai](https://www.anuvad.ai/blog/ai4bharat-indictrans-preprocessing)
[8] [https://arxiv.org](https://arxiv.org/html/2608.08235v2)
[9] [https://www.business-standard.com](https://www.business-standard.com/technology/tech-news/global-ai-models-struggles-with-indian-languages-and-dialects-report-126021600237_1.html)
[10] [https://telanganatoday.com](https://telanganatoday.com/rewind-lost-in-comprehension-can-indias-ai-boom-think-in-its-own-languages)
[11] [https://www.linkedin.com](https://www.linkedin.com/posts/linkedin.com-company-currentmatrix_ai-indiaai-artificialintelligence-activity-7496559289814188032-bnwn)
[12] [https://www.ijert.org](https://www.ijert.org/voice-to-empower-a-multilingual-ai-solution-for-tribal-inclusion-ijertv15is080183)
