# SrcMix: Mixing of Related Source Languages Benefits Extremely Low-resource Machine Translation

📢 **Accepted to EACL 2026 (Findings)**

Official implementation of **SrcMix**, a simple and effective
training-time strategy for improving machine translation in **Extremely
Low-Resource Languages (ELRLs)**.

------------------------------------------------------------------------

## Motivation

Extremely low-resource languages (ELRLs) often suffer from:

-   Fewer than 6K parallel sentences
-   Limited supervision
-   High typological diversity
-   Weak transfer from massively multilingual models

Standard multilingual training (naïve concatenation or many-to-many setups) Often performs poorly in ELRL settings due to:

-   Negative transfer
-   Cross-lingual interference
-   Fragmented decoder supervision

**SrcMix** addresses this by introducing multilinguality only on the
*source side*, while keeping the decoder specialized to a single target
ELRL.

------------------------------------------------------------------------

## What is SrcMix?

Let:

-   Target ELRL: n1
-   Related source languages: n2, n3, ..., nN
-   High-resource language: H

To train H → n1, we mix:

H → n1
n2 → n1
n3 → n1
...
nN → n1

Key design choices:

-   Remove explicit source language identifiers
-   Force implicit structural transfer
-   Preserve decoder specialization

Unlike naïve multilingual mixing, SrcMix prevents decoder fragmentation
and improves performance under extreme data scarcity.

------------------------------------------------------------------------

## 🧡 First Public Angika MT Dataset

This work introduces the **first publicly available machine translation
training and evaluation dataset for Angika**, an Indo-Aryan language
spoken in eastern India.

Dataset available here:

https://huggingface.co/datasets/snjev310/AngikaMT

The dataset includes:

-   Parallel training data
-   Evaluation splits
-   FLORES-aligned dev/test sets
-   Clean preprocessing for reproducibility

------------------------------------------------------------------------

## 📂 Repository Structure

```text
srcmix/
│
├── srcmix/
│   ├── training/
│   │   ├── train_single.py
│   │   ├── train_srcmix.py
│   │   └── train_naive_mix.py
│   │
│   ├── data/
│   │   ├── build_dataset.py
│   │   ├── mixing.py
│   │   └── splits.py
│   │
│   ├── evaluation/
│   │   └── evaluate.py
│   │
│   └── utils/
│       └── config.py
│
├── configs/
├── scripts/
└── README.md
```

------------------------------------------------------------------------

## Training

### Single Supervised Training

bash scripts/run_single.sh

### SrcMix Training

bash scripts/run_srcmix.sh

### Naïve Multilingual Mixing (Baseline)

bash scripts/run_ablations.sh

------------------------------------------------------------------------

## Evaluation

python srcmix/evaluation/evaluate.py --peft_model_path path_to_adapter
--test_data path_to_tokenized_test

Metrics:

-   BLEU (sacreBLEU)
-   ChrF++ 

------------------------------------------------------------------------

## 🔬 Experimental Setup

-   Base Model: Aya-101 (CohereForAI), mT5-Large
-   Fine-tuning: LoRA (r=16)
-   Training data: \~6K sentences per language
-   Evaluation: FLORES-aligned splits
-   Metrics: BLEU and ChrF++

------------------------------------------------------------------------

## Key Contributions

-   Introduce **SrcMix**, a source-side mixing strategy tailored for
    ELRLs.
-   Show that naïve multilingual mixing underperforms in extreme data
    scarcity.
-   Release the first MT training & evaluation dataset for Angika.
-   Provide systematic comparison across language families and scripts.
-   Demonstrate consistent gains across multiple ELRLs.

------------------------------------------------------------------------

## 📜 Citation

If you use this dataset or the associated research in your work, please cite it as follows:

```bibtex
@inproceedings{kumar-etal-2026-srcmix,
    title = "{S}rc{M}ix: Mixing of Related Source Languages Benefits Extremely Low-resource Machine Translation",
    author = "Kumar, Sanjeev  and
      Jyothi, Preethi  and
      Bhattacharyya, Pushpak",
    editor = "Demberg, Vera  and
      Inui, Kentaro  and
      Marquez, Llu{\'i}s",
    booktitle = "Findings of the {A}ssociation for {C}omputational {L}inguistics: {EACL} 2026",
    month = mar,
    year = "2026",
    address = "Rabat, Morocco",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2026.findings-eacl.332/",
    doi = "10.18653/v1/2026.findings-eacl.332",
    pages = "6306--6323",
    ISBN = "979-8-89176-386-9",
}

```
------------------------------------------------------------------------

## 🤝 Acknowledgements

This work was supported by a Ph.D. grant from the TCS Research Foundation and the Amazon-IIT Bombay AI/ML initiative.

------------------------------------------------------------------------

## 📬 Contact

**Sanjeev Kumar** CSE IIT Bombay  
Email: `sanjeev@cse.iitb.ac.in`
