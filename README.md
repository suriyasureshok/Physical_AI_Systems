# AI Systems Engineering – Mini Projects

This repository contains a collection of **small, focused mini projects** designed to build intuition and hands-on experience for an **AI Systems Engineer (SDE-level)** role.

Each project is intentionally scoped to explore how **algorithms, linear algebra, and ML workloads interact with real system constraints** such as:
- Memory usage
- Latency
- Batch size
- Sequence length
- Hardware and OS behavior

The goal is **not** to build large applications, but to develop **systems-level thinking** through controlled experiments.

---

## Motivation

Modern AI systems (especially LLMs) fail or succeed not solely due to model architecture, but because of **system-level constraints**:

- Memory pressure – RAM/VRAM limitations
- Compute scaling – CPU/GPU utilization patterns
- Latency tail behavior – p95/p99 performance characteristics
- Hardware limits – Physical constraints and bottlenecks

### Core Questions This Repository Answers

- Why does increasing embedding dimension hurt latency?
- When does batching stop helping?
- How do sequence length and batch size amplify memory usage?
- Why does latency grow non-linearly even for simple operations?

These are **AI Systems Engineering questions**, not generic ML theory.

---

## Repository Structure

```
MINI_PROJECTS/
│
├── notebooks/
│   ├── week1/
│   │   ├── week_1.ipynb   # Week 1: Embedding Dimension vs Latency & Memory
│   │   └── README.md      # Week 1 documentation
│   └── week2/             # Future experiments
│
├── README.md              # Main project documentation
├── pyproject.toml         # Python project configuration
├── requirements.txt       # Pip dependencies
├── uv.lock                # uv dependency lock file
├── .python-version        # Python version specification
├── .gitignore             # Git ignore rules
└── .venv/                 # Local virtual environment (not committed)
```

---

## Projects

| Week | Mini Project | Focus Area | Status |
|:----:|:------------|:-----------|:------:|
| 1 | Embedding Dimension vs Latency & Memory | System Performance Analysis | Complete |
| 2 | TBD | TBD | Planned |

### Project Characteristics

Each mini project is:
- Time-boxed – Focused and manageable scope
- Experiment-driven – Data and measurement focused
- Single insight – One key systems concept per project
- Well-documented – Clear observations and conclusions

---

### AI Systems Engineer Takeaway

**Key Insight:** Performance in AI systems is governed by interacting factors, not single parameters.

Embedding dimension, batch size, and sequence length multiply together to determine memory footprint and compute cost. Once hardware thresholds are crossed, latency increases non-linearly.

#### Real-World Applications

This insight directly applies to:
- LLM inference serving – Optimizing throughput and latency
- GPU memory planning – Capacity estimation and allocation
- Batch size tuning – Finding the sweet spot for your workload
- System design interviews – Demonstrating production-level thinking

---

## Tech Stack

- **Python 3.10+**
- **PyTorch** – Deep learning framework
- **Pandas** – Data manipulation and analysis
- **Matplotlib** – Visualization
- **Jupyter Notebook** – Interactive experimentation

---

## How to Run

### Prerequisites

- Python 3.10 or higher
- [uv](https://github.com/astral-sh/uv) (recommended) or pip

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Mini_Project_Series
```

### 2. Install Dependencies

#### Using uv (recommended):

```bash
uv sync
```

#### Using pip:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
```

### 3. Run Jupyter Notebook

```bash
jupyter notebook notebooks/week1/week_1.ipynb
```

Or launch Jupyter Lab:

```bash
jupyter lab
```

---

## Future Extensions

Planned enhancements and experiments:

### Performance Analysis
- Latency distribution analysis (p50, p95, p99)
- Throughput measurement (tokens/second, requests/second)
- Tail latency optimization techniques

### Hardware & Optimization
- GPU-based experiments (CUDA profiling)
- Reduced precision (FP16, BF16, INT8 quantization)
- Multi-process and concurrency effects

### Production Scenarios
- Cloud-based inference simulations
- Distributed inference patterns
- Request batching and scheduling strategies

---

## Learning Philosophy

This repository follows a **systems-first learning approach**:

- Measure before optimizing – Data-driven decisions
- Prefer numbers over intuition – Quantitative over qualitative
- Document observations clearly – Reproducible insights
- Treat performance as a system property – Not just code quality

---

## Author

Built as part of a structured **AI Systems Engineering learning path**, focusing on:
- Long-term skill development
- Hardware-aware system design
- Production-ready engineering thinking
- Deep understanding over surface-level knowledge

---

## Disclaimer

These experiments are **educational simplifications** and not intended to replicate full production LLM inference pipelines. They are designed to:
- Build systems-level intuition
- Understand performance characteristics
- Practice measurement and analysis
- NOT benchmark real-world models