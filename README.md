# Detecting Data Poisoning in AI Models: A Curated Survey

> **A curated collection of research papers on detecting and defending against data poisoning and backdoor attacks in deep learning — covering CNNs and LLMs.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Last Updated](https://img.shields.io/badge/Last%20Updated-March%202026-blue.svg)]()

---

## Table of Contents

- [Overview](#overview)
- [Part I — Data Poisoning Detection in CNNs](#part-i--data-poisoning-detection-in-cnns)
  - [Surveys](#surveys)
  - [Detection Methods](#detection-methods)
  - [Defense & Purification](#defense--purification)
  - [Notable Attacks (for context)](#notable-attacks-for-context)
- [Part II — Data Poisoning Detection in LLMs](#part-ii--data-poisoning-detection-in-llms)
  - [Surveys](#surveys-1)
  - [Key Findings](#key-findings)
  - [Attacks by Training Phase](#attacks-by-training-phase)
  - [Attacks on LLM Agents](#attacks-on-llm-agents)
  - [Detection & Defense Methods](#detection--defense-methods)
  - [Benchmarks & Tools](#benchmarks--tools)
  - [Domain-Specific Risks](#domain-specific-risks)
- [Additional Resources](#additional-resources)
- [Contributing](#contributing)

---

## Overview

Data poisoning is one of the most critical threats to machine learning security. An adversary injects malicious samples into training data to manipulate model behavior — either causing targeted misclassifications (backdoor attacks) or degrading overall performance (availability attacks).

This repository compiles key research papers organized into two main tracks:

1. **CNNs (Convolutional Neural Networks):** Detection of poisoned samples via activation analysis, graph-based inspection, and training dynamics.
2. **LLMs (Large Language Models):** Poisoning threats across pre-training, instruction tuning, RLHF, and inference — along with emerging defenses.

Each entry includes a brief description, publication venue (when available), and a direct link to the paper.

---

## Part I — Data Poisoning Detection in CNNs

### Surveys

| Paper | Year | Description |
|-------|------|-------------|
| [Data Poisoning in Deep Learning: A Survey](https://arxiv.org/abs/2503.22759) | 2025 | Comprehensive survey covering attacks (backdoor, triggerless, clean-label), detection methods, and defenses. Tested on MNIST, CIFAR-10, SVHN, Tiny ImageNet, ImageNet with VGG16, ResNet, InceptionV3, MobileNet. |
| [Toward Robust Deep Learning against Poisoning Attacks](https://dl.acm.org/doi/full/10.1145/3574159) | 2023 | ACM tutorial on building robust deep learning pipelines against poisoning attacks. |

### Detection Methods

| Paper | Year | Description |
|-------|------|-------------|
| [DeBUGCN — Detecting Backdoors in CNNs Using Graph Convolutional Networks](https://hf.co/papers/2502.18592) | 2025 | Transforms static CNN weights into graph structures and uses a GCN binary classifier to detect trojaned models. Faster and more accurate than state-of-the-art. Tested on MNIST, CIFAR-10, and the TrojAI dataset. |
| [BaDExpert — Extracting Backdoor Functionality for Accurate Backdoor Input Detection](https://hf.co/papers/2308.12439) | 2023 | Extracts backdoor functionality from a compromised model into a "backdoor expert model" via fine-tuning on mislabeled samples. This expert then serves as a poisoned-input detector. Validated on CIFAR-10, GTSRB, ImageNet with ResNet, VGG, MobileNetV2, and ViT. |
| [UMD — Unsupervised Model Detection for X2X Backdoor Attacks](https://hf.co/papers/2305.18651) | 2023 | First unsupervised method detecting X2X backdoors (arbitrary source-target pairs) via a transferability statistic and trigger reverse-engineering. Outperforms SOTA on CIFAR-10, GTSRB, and Imagenette. |
| [Activation Clustering (AC)](https://ceur-ws.org/Vol-2301/paper_18.pdf) | 2019 | Classic method exploiting the difference in internal network activations — poisoned samples are classified correctly for "wrong reasons" (trigger memorization), creating separable clusters in activation space. |
| [Exploring Model Dynamics for Accumulative Poisoning Discovery](https://hf.co/papers/2306.03726) | 2023 | Introduces "Memorization Discrepancy" — an information-theoretic measure exploiting model dynamics during training to distinguish poisoned from clean samples. Code available on GitHub. |

### Defense & Purification

| Paper | Year | Description |
|-------|------|-------------|
| [PureEBM — Universal Poison Purification via Energy-Based Models](https://hf.co/papers/2405.19376) | 2024 | Universal preprocessing based on Energy-Based Models (EBM) that purifies poisoned images via Langevin sampling. Effective against white-box, gray-box, and black-box poisons. |
| [HINT — Healthy Influential-Noise based Training](https://hf.co/papers/2309.08549) | 2023 | Uses influence functions to generate "healthy noise" that strengthens CNN robustness against targeted and untargeted attacks without degrading generalization. |
| [Backdoor Defense via Suppressing Model Shortcuts](https://hf.co/papers/2211.05631) | 2022 | Exploits skip connections in CNNs (ResNet, etc.) as backdoor vectors and proposes suppressing them in critical layers to neutralize attacks. |

### Notable Attacks (for context)

Understanding attacks is essential for designing effective defenses.

| Paper | Year | Description |
|-------|------|-------------|
| [Poisoning Web-Scale Training Datasets is Practical](https://hf.co/papers/2302.10149) | 2023 | Carlini et al. demonstrate that poisoning LAION-400M costs as little as $60. |
| [Nightshade: Prompt-Specific Poisoning Attacks on Text-to-Image Models](https://hf.co/papers/2310.13828) | 2023 | Targeted prompt-based attack on generative models, effective with fewer than 100 samples. |
| [SAPA — Sharpness-Aware Data Poisoning Attack](https://hf.co/papers/2305.14851) | 2023 | Optimizes the loss landscape to maximize poison persistence across training. |

---

## Part II — Data Poisoning Detection in LLMs

### Surveys

| Paper | Year | Description |
|-------|------|-------------|
| [A Survey on Backdoor Threats in Large Language Models](https://arxiv.org/abs/2502.05224) | 2025 | The most comprehensive and recent survey. Structures threats across three LLM lifecycle phases: pre-training, fine-tuning/RLHF, and inference. Covers attacks, defenses, and evaluation methods. |
| [Breaking Down the Defenses: A Comparative Survey of Attacks on LLMs](https://hf.co/papers/2403.04786) | 2024 | Categorizes LLM vulnerabilities into "The Good" (beneficial uses), "The Bad" (offensive uses), and "The Ugly" (intrinsic flaws). |
| [LLM Security and Privacy: The Good, the Bad, and the Ugly](https://hf.co/papers/2312.02003) | 2023 | Explores the intersection of LLMs, security, and privacy, including data poisoning and parameter extraction. |

### Key Findings

| Paper | Year | Description |
|-------|------|-------------|
| [Poisoning Attacks on LLMs Require a Near-Constant Number of Poison Samples](https://hf.co/papers/2510.07192) | 2025 | **Critical result:** Only ~250 poisoned documents are needed to compromise a model, regardless of dataset size (6B–260B tokens) or model size (600M–13B parameters). The number of required poisons does not scale with model size. |
| [Persistent Pre-Training Poisoning of LLMs](https://proceedings.iclr.cc/paper_files/paper/2025/file/4dade38eae8c007f3a564b8ea820664a-Paper-Conference.pdf) | 2025 | ICLR 2025. Shows that poison effects injected during pre-training can persist through subsequent stages (instruction tuning, RLHF), making the threat even more severe. |

### Attacks by Training Phase

#### Pre-training Poisoning

Pre-training on massive web corpora (Common Crawl, LAION, etc.) is particularly vulnerable — adversaries can modify indexed web content at low cost to inject poisoned data into future training runs.

#### Fine-tuning (SFT) Poisoning

| Paper | Year | Description |
|-------|------|-------------|
| [Learning to Poison LLMs for Downstream Manipulation (GBTL)](https://hf.co/papers/2402.13459) | 2024 | Gradient-guided backdoor trigger learning targeting supervised fine-tuning. Tested on sentiment analysis, domain generation, and QA. Also proposes two defenses: in-context learning (ICL) and continuous learning (CL). |

#### RLHF Poisoning

| Paper | Year | Description |
|-------|------|-------------|
| [Reward Poisoning Attack for Reinforcement Learning](https://aclanthology.org/2024.acl-long.140.pdf) | 2024 | ACL 2024. Poisons preference data used to train the RLHF reward model. Even a small fraction of corrupted data causes the final model to consistently generate harmful content. |

#### Multi-turn Chat & Stealth Attacks

| Paper | Year | Description |
|-------|------|-------------|
| [Exploring Backdoor Vulnerabilities of Chat Models](https://hf.co/papers/2404.02406) | 2024 | Exploits multi-turn conversational format to distribute triggers across multiple user messages, making detection much harder. Achieves >90% ASR on Vicuna-7B; backdoor survives realignment. |
| [Revisiting Backdoor Attacks on LLMs: A Stealthy Framework via Harmless Inputs](https://arxiv.org/abs/2505.17601) | 2025 | Uses only benign QA data to establish associations between triggers and affirmative prefixes — no harmful content is ever exposed during training. Extremely difficult to detect. |

### Attacks on LLM Agents

| Paper | Year | Description |
|-------|------|-------------|
| [BadAgent](https://hf.co/papers/2406.03007) | 2024 | Shows that LLM agents with external tool access (APIs, browser, etc.) become especially dangerous once compromised — backdoors can trigger real-world actions (purchases, data manipulation, code execution). |
| [Watch Out for Your Agents!](https://hf.co/papers/2402.11208) | 2024 | Demonstrates vulnerabilities in agentic LLM pipelines. |
| [AutoBackdoor](https://hf.co/papers/2511.16709) | 2025 | Fully automates the attack pipeline via an LLM agent: trigger generation, poisoned data construction, fine-tuning. Achieves >90% ASR on LLaMA-3, Mistral, Qwen, and GPT-4o. |

### Detection & Defense Methods

| Paper | Year | Description |
|-------|------|-------------|
| [From Poisoned to Aware: Fostering Backdoor Self-Awareness in LLMs](https://hf.co/papers/2510.05169) | 2025 | Novel approach training the poisoned model to become "self-aware" of its own backdoor via inverse reinforcement learning. The model identifies its own triggers. Emergence resembles a phase transition. |
| [Mitigating Backdoor Threats to Large Language Models](https://arxiv.org/abs/2409.19993) | 2024 | Review of mitigation strategies including data filtering, activation analysis-based detection, and post-training purification techniques. |
| [Measuring Impacts of Poisoning on Model Parameters and Neuron Activations](https://hf.co/papers/2402.12936) | 2024 | White-box study on CodeBERT showing that activation values and contextual embeddings exhibit detectable patterns — but not attention weights. |
| [Multi-Faceted Studies on Data Poisoning can Advance LLM Development](https://arxiv.org/abs/2502.14182) | 2025 | Argues that studying data poisoning is not only defensive but can also advance LLM development (understanding curriculum learning, memorization dynamics, etc.). |

### Benchmarks & Tools

| Paper | Year | Description |
|-------|------|-------------|
| [BackdoorLLM (NeurIPS 2025)](https://hf.co/papers/2408.12798) | 2025 | First comprehensive benchmark for LLM backdoors. Includes 200+ experiments, 8 attack types, 7 scenarios, and 6 model architectures. Open-source: [GitHub](https://github.com/bboylyg/BackdoorLLM). |

### Domain-Specific Risks

| Paper | Year | Description |
|-------|------|-------------|
| [Medical LLMs are Vulnerable to Data-Poisoning Attacks](https://www.nature.com/articles/s41591-024-03445-1) | 2024 | Published in *Nature Medicine*. Shows that replacing only **0.001%** of training tokens with medical disinformation is sufficient to produce a model that propagates medical errors. |

---

## Additional Resources

- [Awesome Data Poisoning and Backdoor Attacks](https://github.com/penghui-yang/awesome-data-poisoning-and-backdoor-attacks) — Curated GitHub list of papers and resources (no longer maintained but still valuable).
- [Data Poisoning, Backdoor Attacks, and Defenses (Goldblum et al., 2020)](https://arxiv.org/abs/2012.10544) — Early comprehensive overview of the field.

---

## Contributing

Contributions are welcome! If you know of a relevant paper not listed here, please open an issue or submit a pull request.

When adding a paper, please include:
- Paper title with a link to the source (arXiv, conference proceedings, etc.)
- Year of publication
- A brief description (1–3 sentences)
- The appropriate section (CNN / LLM, Attack / Detection / Defense)

---

## Citation

If you find this resource useful for your research, please consider giving it a star and citing it:

```bibtex
@misc{data-poisoning-detection-survey,
  title={Detecting Data Poisoning in AI Models: A Curated Survey},
  year={2026},
  url={https://github.com/YOUR_USERNAME/data-poisoning-detection-survey}
}
```

---

*Last updated: March 2026*
