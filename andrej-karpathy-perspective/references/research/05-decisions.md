# Andrej Karpathy — Major Decisions & Key Actions

> Research date: 2026-04-29
> Source note: Based on training data + Wikipedia verification

---

## I. Career Decisions

### 1. Choosing OpenAI over Industry (2015)
- **Context**: After PhD graduation, offers from multiple tech companies and academia
- **Decision**: Chose OpenAI (just founded at the time) as an early employee
- **Logic**: "Wanted to do research不受 constrained by commercial pressure"
- **Retrospective reflection**: Has expressed publicly multiple times that the OpenAI experience was "extremely valuable"
- **Source**: Type: Second-hand (interviews/reports), Credibility: Medium

### 2. Joining Tesla for Autopilot (2017)
- **Context**: After success at OpenAI, Elon Musk personally invited him
- **Decision**: Left a comfortable research position to join Tesla and lead autonomous driving vision
- **Logic**: "Wanted to apply deep learning to the physical world" — from the virtual internet to real cars
- **Action**: Built and led a 100+ person vision team
- **Source**: Type: First-hand (Tesla AI Day talks) + Second-hand (reports), Credibility: Medium-high

### 3. Leaving OpenAI (January 2024)
- **Context**: Announced departure suddenly after nearly 9 years at OpenAI
- **Expression**: Just posted a tweet "the end [GIF]" — extremely brief
- **Aftermath**: Founded Eureka Labs (2024), an AI education platform
- **Inferred logic**: Choosing education entrepreneurship over joining another company reflects his continued pursuit of "educational impact"
- **Source**: First-hand (Twitter) + public statement, Credibility: High

### 4. Choosing D&E over Research Role at OpenAI
- **Context**: Among early OpenAI employees, Karpathy was assigned to the engineering track
- **Decision**: Accepted the Director of Engineering role
- **Logic**: He was already inclined toward engineering practice (evident from his blog and open-source projects), and this role let him leverage his strength in "engineering-izing research"
- **Source**: Type: Second-hand (industry analysis), Credibility: Medium

---

## II. Project Decisions

### 5. Creating CS231n Course Notes (2016)
- **Decision**: Spent time writing a complete set of CNN lecture notes
- **Logic**: "The best way to learn is to teach"
- **Result**: Became the most widely used deep learning tutorial globally

### 6. Choosing the "Build from Scratch" Video Approach (2020-2023)
- **Decision**: Instead of making polished tutorials, go with single-take live coding
- **Logic**: "If you want to prove you really understand it, write it live"
- **Result**: This format became his signature style, millions of views

### 7. Creating nanoGPT (2022)
- **Decision**: Compress the GPT implementation to ~300 lines of Python
- **Logic**: "If someone asks me how GPT works, rather than explaining a thousand times, better to give them working code"
- **Result**: Became the most popular way to understand GPT internals

### 8. Creating llm.c (2023)
- **Decision**: Rewrite LLM training in pure C, no framework dependencies
- **Logic**: "If you can't run it without a GPU, do you really understand it?"
- **Result**: Trained a GPT on an M1 MacBook, proof of concept

### 9. microGPT Project (February 2026)
- **Decision**: Compress GPT further to 200 lines
- **Logic**: Continued pursuit of minimalism, "I cannot make this any shorter"
- **Source**: Blog post confirmation, Credibility: High

---

## III. Words-Actions Consistency Analysis

### Consistent areas:
- "Simplicity first" — consistent from micrograd (~100 lines) → nanoGPT (~300 lines) → llm.c (pure C) → microGPT (200 lines)
- "Understand by building" — practiced it himself and taught it to others
- "Data > architecture" — this philosophy was reflected in Tesla's data engine design

### Inconsistent areas:
- Advocates "open-source education" while also deeply participating in Tesla Autopilot (closed-source commercial project) confidentiality
- Attitude toward AI safety: actively engaged in discussion early on, less vocal later — may be role change, may be立场 evolution

---

## IV. Retrospective Reflections & Learnings

### Publicly shared reflections:
1. "A Survival Guide to a PhD" — lessons learned from his own PhD experience
2. Tesla AI Day — shared lessons from the Autopilot transition from pipeline to end-to-end learning
3. Recipe essay — universal methodology distilled from countless debugging sessions

### Not shared:
- The specific reason for leaving OpenAI (only said "the end")
- Views on OpenAI internal governance controversies (silent)


