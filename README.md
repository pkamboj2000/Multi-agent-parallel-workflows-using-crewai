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

## 🚀 Features

- **Parallel Processing**: Uses `ThreadPoolExecutor` for concurrent web searches
- **Multi-Source Aggregation**: Combines reviews from 3+ automotive sources
- **AI-Powered Synthesis**: Creates comprehensive, non-redundant final reviews
- **Customizable Topics**: Easy to change vehicle/topic for review
- **Rate Limiting**: Built-in delays to respect website policies

---

## 📋 Requirements

```bash
pip install crewai
pip install langchain-community
pip install duckduckgo-search
```

### Environment Variables
```bash
export GROQ_API_KEY="your-groq-api-key-here"
```

---

## 🛠️ Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd automotive-review-aggregator
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   ```bash
   # Create .env file
   echo "GROQ_API_KEY=your-groq-api-key" > .env
   ```

4. **Run the notebook**
   ```bash
   jupyter notebook code.ipynb
   ```

---

## 🎯 Usage

### Basic Usage
1. Open `code.ipynb` in Jupyter
2. Set your desired topic:
   ```python
   topic = "2024 Honda Civic review"  # Change this to any vehicle
   ```
3. Run all cells to get comprehensive review

### Custom Topics
Simply modify the topic variable:
```python
topic = "2025 Toyota Camry review"
topic = "2024 BMW X3 reliability"
topic = "Ford F-150 Lightning range test"
```

---

## ⚡ Performance

- **Sequential Execution**: ~21 seconds
- **Parallel Execution**: ~7 seconds  
- **Speed Improvement**: 66% faster processing

---

## 🔧 Technical Details

### Agent Configuration
- **LLM**: Groq Qwen 3-32B (fast inference)
- **Search Tool**: DuckDuckGo (rate-limited)
- **Concurrency**: ThreadPoolExecutor with 3 workers

### Parallel Processing Implementation
```python
with ThreadPoolExecutor(max_workers=3) as executor:
    future_t1 = executor.submit(run_task_in_parallel, t1, reviewer1)
    future_t2 = executor.submit(run_task_in_parallel, t2, reviewer2) 
    future_t3 = executor.submit(run_task_in_parallel, t3, reviewer3)
```

---
