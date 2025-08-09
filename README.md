# 🚗 Automotive Review Crew — Parallel + Sequential Multi-Agent Workflow

This project demonstrates a **multi-agent system** built with [`CrewAI`](https://github.com/joaomdmoura/crewai) to produce a **single, unbiased automotive review**.  
It combines **parallel information gathering** with **sequential synthesis** to deliver a concise report with sources.

---

## 📜 Overview

**Two-stage workflow:**

1) **Parallel Information Gathering** — three reviewer agents run *at the same time* on different sites.  
2) **Sequential Synthesis** — a fourth agent (the **Synthesizer**) waits for the three results and produces the final report.

---

## 👥 Agents at a Glance

| Agent        | Source(s)                           | Role                                                            |
|--------------|-------------------------------------|------------------------------------------------------------------|
| `reviewer1`  | Edmunds                             | Extracts pros/cons, key highlights, and link(s)                 |
| `reviewer2`  | Car and Driver                      | Extracts pros/cons, key highlights, and link(s)                 |
| `reviewer3`  | Top Gear / Autocar / What Car       | Extracts pros/cons, unique perspectives, and link(s)            |
| `synthesizer`| **All three reviewers (context)**   | **Combines everything into consensus bullets + final verdict + agreement/differences** |

---

## 💡 Why Parallel + Multi-Source? (Benefits)

- **Saves time:** running three reviewers **in parallel** cuts wall-clock time compared to visiting sites one by one.  
- **Reduces bias:** no single outlet can “trap” the result; the summarizer compares multiple sources and surfaces **consensus vs. disagreement**.  
- **More robust:** if one site is slow, blocked, or low-quality, the other agents still complete, so the final report doesn’t fail.  
- **Broader coverage:** different publications emphasize different aspects (performance, comfort, tech, value), giving a fuller picture.  
- **Traceable:** each reviewer returns **plain URLs**, so readers can audit the sources directly.

---

## ⚙️ Execution Model

### 1️⃣ Parallel Reviewers
Reviewer tasks are marked asynchronous so they **run simultaneously**:
```python
t1.async_execution = True
t2.async_execution = True
t3.async_execution = True

