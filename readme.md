# Nwāchā Munā: A Devanagari Speech Corpus and Proximal Transfer Benchmark for Nepal Bhasha ASR

> Nwāchā Munā (/nwa:tSa: muna:/) means “speech corpus” or "collection of speech" in Nepal Bhasha (Newari).

---

Authors: Rishikesh Kumar Sharma, Safal Narshing Shrestha, Jenny Poudel, Rupak Tiwari, Arju Shrestha, Rupak Raj Ghimire, Bal Krishna Bal<br>
Information and Language Processing Research Lab (ILPRL)<br>
Kathmandu University, Nepal


## Abstract

Nepal Bhasha (Newari), an endangered language of the Kathmandu Valley, remains digitally marginalized due to the severe scarcity of annotated speech resources. In this work, we introduce **Nwāchā Munā**, a newly curated **5.39-hour manually transcribed Devanagari speech corpus** for Nepal Bhasha, and establish the first benchmark using script-preserving acoustic modeling.

We investigate whether **proximal cross-lingual transfer** from a geographically and linguistically adjacent language (Nepali) can rival large-scale multilingual pretraining in an ultra-low-resource Automatic Speech Recognition (ASR) setting. Fine-tuning a Nepali Conformer model reduces the Character Error Rate (CER) from a **52.54% zero-shot baseline to 17.59%** with data augmentation, effectively matching the performance of the multilingual Whisper-Small model despite utilizing significantly fewer parameters.

Our findings demonstrate that proximal transfer within South Asian language clusters serves as a computationally efficient alternative to massive multilingual models. We openly release the dataset and benchmarks to digitally enable the Newari community and foster further research in Nepal Bhasha.

**Preprint:**  arXiv: [Read](https://arxiv.org/abs/2603.07554)

**Full Paper:** *To be linked upon publication at CHiPSAL @ LREC 2026*


## Introduction

Nepal Bhasha (Newari) is spoken by over **860,000 people** in Nepal and holds official working language status in Bagmati Province. Despite a six-century-old history, it is classified by UNESCO as a **"definitely endangered"** language — a stark contrast to its cultural significance. In a country with 124 official languages, the absence of digital speech tools for indigenous languages like Newari widens an already deep divide.

This work takes a direct step toward closing that gap. We curate the first large-scale Devanagari-script speech corpus for Nepal Bhasha and establish a rigorous ASR benchmark. Crucially, we ask a question with broad implications for the region: *can a model trained on a neighboring language like Nepali — sharing the same script and acoustic neighborhood — substitute for the massive compute and data demands of multilingual models like Whisper?*


## Key Takeaways

### 1. Proximal Transfer Works — and Works Efficiently
A Conformer model pre-trained on Nepali and fine-tuned on just 5.39 hours of Newari speech achieves a **CER of 18.72%**, matching the fine-tuned Whisper-Small model (18.76%) — a model 5× larger and backed by orders of magnitude more multilingual training data. Shared Devanagari script and acoustic similarity between the two languages make this possible.

### 2. Data Augmentation is Critical in Ultra-Low-Resource Settings
Augmenting the 5.39-hour corpus (speed perturbation, pitch shifting, noise injection) expanded the effective training data to 23.05 hours and pushed the best CER down to **17.59%**, the top result across all experiments. When data is scarce, augmentation can close the gap that raw scale cannot.

### 3. Zero-Shot Transfer Alone is Not Enough
Despite sharing the Devanagari script, the zero-shot NepConformer achieves only **52.54% CER** on Newari — confirming that phonological distinctiveness between the two languages requires explicit fine-tuning. Script sharing is a useful head-start, not a free pass.

### 4. The Encoder Generalizes; the Decoder Adapts
Freezing the Nepali encoder and fine-tuning only the decoder yields **18.77% CER** — nearly identical to full model fine-tuning. This suggests the Nepali acoustic encoder already captures representations transferable to Newari, reducing the compute cost of adaptation without sacrificing quality.

### 5. Pseudo-Labeling Hurts When Domains Don't Match
A semi-supervised experiment incorporating 9.33 hours of filtered broadcast audio (radio, podcasts, TV) *degraded* performance to 19.83% CER. In ultra-low-resource settings, **domain alignment matters more than raw data volume**. Noisy, out-of-domain pseudo-labels can outweigh the gains of additional data.

### 6. Language Model Fusion Improves Words, Not Always Characters
Integrating a 5-gram KenLM via shallow fusion reduced WER by ~11.7% relative, reflecting better word-level consistency. However, CER slightly increased, as the language model occasionally overrides phonetically valid but non-standard local Newari forms — a known tension in agglutinative, low-resource languages.



## The Nwāchā Munā Corpus at a Glance

| Metric | Value |
|---|---|
| Total Duration | 5.39 hours |
| Total Utterances | 5,727 |
| Total Word Tokens | 27,644 |
| Unique Words | 8,599 |
| Number of Speakers | 18 (10M / 8F) |
| Script | Devanagari |
| Domains | Formal text, daily conversation, broadcast |

Data was collected from **18 native speakers** across Banepa, Dhulikhel, Panauti, and Patan, stratified by age and gender to ensure community representation.


## Citation

If you use Nwāchā Munā in your research, please cite:

```bibtex
@inproceedings{sharma2026nwachamuna,
  title     = {Nw\={a}ch\={a} Mun\={a}: A Devanagari Speech Corpus and Proximal Transfer Benchmark for Nepal Bhasha ASR},
  author    = {Sharma, Rishikesh Kumar and Shrestha, Safal Narshing and Poudel, Jenny
               and Tiwari, Rupak and Shrestha, Arju and Ghimire, Rupak Raj and Bal, Bal Krishna},
  booktitle = {Proceedings of CHiPSAL @ LREC2026},
  year      = {2026},
  url       = "https://arxiv.org/abs/2603.07554",
}
```

