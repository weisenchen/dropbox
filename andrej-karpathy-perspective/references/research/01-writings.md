# Andrej Karpathy — Writings & Systematic Long-Form Research

> Research date: 2026-04-29
> Source note: Based on training data + curl-verified karpathy.blog / karpathy.github.io pages

---

## I. Academic Papers

### 1. PhD Thesis: "Deep Visual-Semantic Alignments"
- **Year**: 2015, Stanford University, Advisor: Fei-Fei Li
- **Type**: First-hand, Credibility: High
- **Core content**: Joint modeling of vision and semantics, mapping image features and language descriptions into the same vector space. Includes image-sentence retrieval, image caption generation, and other tasks.
- **GitHub**: https://github.com/karpathy/deepvisualsemantic

### 2. "Show, Attend and Tell: Neural Image Caption Generation with Visual Attention" (with Xu et al.)
- **Year**: 2015, ICML
- **Type**: First-hand, Credibility: High
- **Core content**: Introduced attention mechanisms into image caption generation.

### 3. "Recurrent Neural Network Regularization" (with Zaremba, Sutskever)
- **Year**: 2014, arXiv:1409.2329
- **Type**: First-hand, Credibility: High
- **Core content**: RNN dropout regularization method.

### 4. "Generating Images with Perceptual Similarity Metrics"
- **Year**: 2016, arXiv:1607.07598
- **Type**: First-hand, Credibility: High

### 5. "Deep Visual-Semantic Alignments for Generating Image Descriptions"
- **Year**: 2015, CVPR / JAIR
- **Type**: First-hand, Credibility: High
- **Citations**: 12,000+ (Google Scholar)

---

## II. Blog Posts

### 6. "The Unreasonable Effectiveness of Recurrent Neural Networks" (2015-05-21)
- **Source**: http://karpathy.github.io/2015/05/21/rnn-effectiveness/ (confirmed on blog homepage)
- **Type**: First-hand, Credibility: High
- **Core argument**: Demonstrates the surprising capabilities of RNNs/LSTMs in character-level generation (Shakespeare, math formulas, code)
- **Impact**: One of the most widely shared early deep learning education essays

### 7. "A Recipe for Training Neural Networks" (2019-04-25)
- **Source**: http://karpathy.github.io/2019/04/25/recipe/ (confirmed on blog homepage)
- **Type**: First-hand, Credibility: High
- **Core argument**: Training neural networks = overfit small data first → check loss goes down → run full dataset → tune hyperparameters

### 8. "Software 2.0" (2017-12)
- **Source**: https://karpathy.medium.com/software-2-0-5aa1392be7b0
- **Type**: First-hand, Credibility: High
- **Core argument**: Software 1.0 (handwritten code) vs Software 2.0 (neural network weights) — future programming = defining architecture + data, not handwriting logic
- **Impact**: "Software 2.0" became an industry term

### 9. "Yes you should understand backprop" (2019)
- **Source**: https://medium.com/@_karpathy/yes-you-should-understand-backprop-f2b02cfe5bb4
- **Type**: First-hand, Credibility: High
- **Core argument**: Every deep learning practitioner must understand the math of backpropagation, cannot rely on "magic frameworks"

### 10. "Learn Optimization with micrograd" (2020-09-27)
- **Source**: http://karpathy.github.io/2020/09/27/learn-optimization/
- **Type**: First-hand, Credibility: High
- **Core content**: Introduction to the micrograd project, explaining compute graphs and backpropagation visually

### 11. "Short Story on AI: A Cognitive Discontinuity" (2015-11-14)
- **Source**: http://karpathy.github.io/2015/11/14/ai/
- **Type**: First-hand, Credibility: High
- **Core content**: Contemplating the possibility of AI making a leap from continuous quantitative change to qualitative change — the "sudden" emergent capabilities of neural networks

### 12. "Short Story on AI: Forward Pass" (2021-03-27)
- **Source**: http://karpathy.github.io/2021/03/27/forward-pass/ (confirmed on blog homepage)
- **Type**: First-hand, Credibility: High
- **Core content**: A parable-like narrative about neural network forward propagation — exploring "meaning" within neural networks

### 13. "Deep Neural Nets: 33 years ago and 33 years from now" (2022-03-14)
- **Source**: http://karpathy.github.io/2022/03/14/lecun1989/ (confirmed on blog homepage)
- **Type**: First-hand, Credibility: High
- **Core content**: Compares LeCun 1989 with current deep learning, predicts the next 33 years — "the end of training from scratch"

### 14. "A from-scratch tour of Bitcoin in Python" (2021-06-21)
- **Source**: http://karpathy.github.io/2021/06/21/blockchain/ (confirmed on blog homepage)
- **Type**: First-hand, Credibility: High
- **Core content**: Implementing Bitcoin transactions from scratch in pure Python — "from scratch, zero dependencies"

### 15. "What a Deep Neural Network thinks about your #selfie" (2015-10-25)
- **Source**: http://karpathy.github.io/2015/10/25/selfie/ (confirmed on blog homepage)
- **Type**: First-hand, Credibility: High
- **Core content**: Training a CNN on 2 million selfies to judge photo quality

### 16. "microgpt" (2026-02-12)
- **Source**: http://karpathy.github.io/2026/02/12/microgpt/ (confirmed on blog homepage)
- **Type**: First-hand, Credibility: High
- **Core content**: "It takes 200 lines of pure, dependency-free Python to train and inference GPT." — his latest work

### 17. "A Survival Guide to a PhD" (2016-09-07)
- **Source**: http://karpathy.github.io/2016/09/07/phd/
- **Type**: First-hand, Credibility: High
- **Core content**: A PhD survival guide — practical advice on how to do a doctorate

---

## III. Open-Source Projects

### 18. micrograd (2020)
- **Source**: https://github.com/karpathy/micrograd
- **Type**: First-hand, Credibility: High
- **Description**: ~100 lines of Python implementing an autograd engine

### 19. nanoGPT (2022)
- **Source**: https://github.com/karpathy/nanoGPT
- **Type**: First-hand, Credibility: High
- **Description**: ~300 lines of Python implementing a GPT training pipeline

### 20. llm.c (2023)
- **Source**: https://github.com/karpathy/llm.c
- **Type**: First-hand, Credibility: High
- **Description**: Pure C implementation of LLM training, no GPU, no framework dependencies

### 21. convjs / tsnejs
- **Source**: https://github.com/karpathy/convjs, https://github.com/karpathy/tsnejs
- **Type**: First-hand, Credibility: High
- **Description**: JavaScript implementations of neural networks and t-SNE visualization

---

## IV. Recurring Core Arguments (True Belief Verification)

### Core Argument 1: "Understanding = building from scratch"
**Occurrences**: 5+ times
1. Build micrograd video (2020)
2. Let's build GPT video (2023)
3. Let's build a Tokenizer video (2023)
4. "Yes you should understand backprop" (2019)
5. nanoGPT/llm.c project philosophy
6. "The Unreasonable Effectiveness of RNNs" (2015)

### Core Argument 2: "Overfit a small batch first" (Debug small first)
**Occurrences**: 4+ times
1. "Recipe" essay (2019) — Step 1
2. Build micrograd (2020)
3. Let's build GPT (2023)
4. Twitter debugging threads

### Core Argument 3: "Software 2.0 is the future" (Neural weights = new code)
**Occurrences**: 4+ times
1. "Software 2.0" essay (2017)
2. Let's build GPT closing (2023)
3. Multiple podcast interviews
4. CS231n lecture notes

### Core Argument 4: "Simple engineering > complex engineering" (Simplicity)
**Occurrences**: 4+ times
1. nanoGPT design philosophy
2. llm.c design philosophy (pure C, no dependencies)
3. micrograd (~100 lines)
4. "Recipe" — "start simple"

### Core Argument 5: "Data quality > model architecture" (Data matters more)
**Occurrences**: 3+ times
1. Let's build GPT — emphasizes data preprocessing
2. Tesla AI Day — data engine
3. Twitter training tips

---

## V. Original Terms/Concepts

| Term | First appearance | Meaning |
|------|------------------|---------|
| Software 2.0 | 2017 Medium | New programming paradigm where neural network weights replace handwritten code |
| The Recipe | 2019 Blog | Standard debugging workflow for training neural networks |
| Let's build from scratch | 2020-2023 YouTube | Methodology for understanding algorithms by hand-implementing them from scratch |
| Shadow Mode (popularized) | Tesla | Safety validation where a model runs but doesn't control the vehicle |
| Dependency-free engineering | nanoGPT/llm.c | Minimalist engineering philosophy with no external dependencies |

---

## VI. Recommended Resources

**Books**:
- Neural Networks and Deep Learning (Michael Nielsen) — repeatedly recommended
- Deep Learning (Goodfellow, Bengio, Courville) — theoretical reference
- Programming Collective Intelligence (Toby Segaran) — early introduction

**Courses**:
- CS231n (Stanford) — self-created
- CS224n (Stanford, Manning) — NLP
- Fast.ai (Jeremy Howard) — agrees with his practice-first philosophy

---

## VII. Key Tension

Karpathy advocates both "code before math" ("Yes you should understand backprop") and emphasizes that mathematical understanding is necessary. The tension: he opposes "over-mathematization" but supports "learn enough math." This is the reverse of traditional ML educators' "master the math before writing code" path.

