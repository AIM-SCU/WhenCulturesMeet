# When Cultures Meet: Multicultural Text-to-Image Generation

This repository contains the code and data for our paper:

> **[When Cultures Meet: Multicultural Text-to-Image Generation](https://arxiv.org/pdf/2502.15972)**
> Parth Bhalerao, Oana Ignat, Brian Trinh, Mounika Yalamarty
> *ACL Findings 2026*

![Idea Architecture](images/overview2.png)

---

## Overview

We introduce **multicultural text-to-image generation** as a new task, where a person from one cultural background is depicted in the context of a landmark from a different culture. We present **MosAIG**, a Multi-Agent framework for Image Generation that leverages LLMs with distinct cultural personas to generate richer, more culturally grounded image captions.

Our benchmark contains **9,000 images** spanning:
- 5 countries (United States, Germany, India, Spain, Vietnam)
- 5 languages (English, Hindi, German, Spanish, Vietnamese)
- 3 age groups (Child, Adult, Elder)
- 2 genders (Male, Female)
- 25 historical landmarks

---

## Repository Structure

```
MosAIG/
├── Alt/                            # AltDiffusion image generation pipeline
│   ├── AltDiffusion-m18-Running-Instructions.pdf
│   ├── BatchImageGenerationAltDiffusion.py
│   ├── PromptTranslation.py
│   ├── RunAltExtended.py
│   ├── main-2.py
│   └── main-3.py
├── Flux/                           # FLUX image generation pipeline
│   ├── BatchImageGenerationFlux.py
│   └── FluxNotebook.zip
├── Metrics-Code/                   # Evaluation metrics
│   ├── Metrics-1.py
│   ├── Metrics-2.py
│   ├── Metrics-3.ipynb
│   └── Metrics-4.ipynb
├── Multi-Agent-Setup/              # MosAIG multi-agent framework
│   ├── Final-Multi-V2.py
│   └── Simple-Crew-Setup.py
├── Single Agent Hardcoded Prompts/ # Simple baseline
│   └── SingleHardcoded-Prompts.py
├── data/                           # Metadata and example data
│   ├── example_data/
│   ├── Alt_MultiAgent.xlsx
│   ├── Alt_Simple.xlsx
│   ├── Flux_Multiagent.xlsx
│   └── Flux_Simple.xlsx
└── images/                         # Sample generated images
```

---

## Dataset

The full dataset of 9,000 images along with metadata is available on HuggingFace:

🤗 **[AIM-SCU/Multi-Cultural-Single-Multi-Agent-Images](https://huggingface.co/datasets/AIM-SCU/Multi-Cultural-Single-Multi-Agent-Images)**

The `data/` folder in this repository contains the metadata spreadsheets with image captions and demographic keywords for all four model settings:
- `Alt_MultiAgent.xlsx` — AltDiffusion multi-agent captions
- `Alt_Simple.xlsx` — AltDiffusion simple captions
- `Flux_Multiagent.xlsx` — FLUX multi-agent captions
- `Flux_Simple.xlsx` — FLUX simple captions

---

## MosAIG Framework

MosAIG is a model-agnostic multi-agent prompting framework that decomposes cultural and demographic reasoning across three specialized agents:

- **Country Agent** — describes culturally appropriate attire and accessories
- **Landmark Agent** — describes architectural and environmental details
- **Age-Gender Agent** — describes demographic-specific physical traits

These agents interact over two rounds of conversation, supervised by a **Moderator Agent**, and the outputs are summarized by a **Summarizer Agent** into a final image caption (≤77 tokens).

The framework is implemented using [CrewAI](https://www.crewai.com/open-source) and LLaMA 3.1-8B.

---

## Models

We evaluate four model configurations:

| Model | Description |
|-------|-------------|
| **Alt-S** | AltDiffusion + simple prompt |
| **Alt-M** | AltDiffusion + multi-agent prompt |
| **Flux-S** | FLUX + simple prompt |
| **Flux-M** | FLUX + multi-agent prompt |

- **AltDiffusion** (`BAAI/AltDiffusion-m18`): multilingual open-source T2I model supporting 18 languages
- **FLUX** (`Freepik/flux.1-lite-8B-alpha`): state-of-the-art English-language T2I model

---

## Evaluation Metrics

We evaluate across five dimensions:

| Metric | Description |
|--------|-------------|
| **Alignment** | CLIPScore — text-image semantic correspondence |
| **Quality** | Inception Score — visual fidelity and diversity |
| **Aesthetics** | SigLIP-based aesthetic predictor (1–10 scale) |
| **Knowledge** | Sensitivity to landmark identity via caption swapping |
| **Fairness** | Consistency of performance across demographic substitutions |

---

## Requirements

Install the required packages:

    pip install crewai
    pip install diffusers transformers accelerate
    pip install torch torchvision
    pip install openai-clip
    pip install pandas openpyxl

---

## Citation

If you use this work, please cite:

@inproceedings{bhalerao-etal-2026-cultures,
    title = "When Cultures Meet: Multicultural Text-to-Image Generation",
    author = "Bhalerao, Parth  and
      Ignat, Oana  and
      Trinh, Brian  and
      Yalamarty, Mounika",
    editor = "Liakata, Maria  and
      Moreira, Viviane P.  and
      Zhang, Jiajun  and
      Jurgens, David",
    booktitle = "Findings of the {A}ssociation for {C}omputational {L}inguistics: {ACL} 2026",
    month = jul,
    year = "2026",
    address = "San Diego, California, United States",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2026.findings-acl.1783/",
    doi = "10.18653/v1/2026.findings-acl.1783",
    pages = "35808--35828",
    ISBN = "979-8-89176-395-1",
    abstract = "Text-to-image generation models have achieved strong performance in culturally homogeneous settings, yet their ability to generate multicultural scenes{---}where people and landmarks originate from different cultures{---}remains largely unexplored. We introduce multicultural text-to-image generation as a new task and present the first benchmark designed to study this setting. Our dataset contains 9,000 images spanning five countries, three age groups, two genders, 25 historical landmarks, and five languages. Using this benchmark, we analyze the behavior of state-of-the-art text-to-image models across multiple dimensions, including alignment, image quality, aesthetics, knowledge, and fairness. As one strategy for composing cultural and demographic information, we explore MosAIG, a Multi-Agent framework that enhances multicultural image generation by leveraging large language models with distinct cultural personas. Our analysis shows that richer prompt composition can improve image quality and cultural grounding compared to simple prompts, while also revealing substantial disparities across languages and demographic groups. We release our dataset and code at https://github.com/AIM-SCU/MosAIG"
}

---

## Links

- 📄 **Paper**: [ACL Findings 2026](https://arxiv.org/pdf/2502.15972)
- 🤗 **Dataset**: [HuggingFace](https://huggingface.co/datasets/AIM-SCU/Multi-Cultural-Single-Multi-Agent-Images)
- 💻 **Code**: [GitHub](https://github.com/AIM-SCU/MosAIG)
