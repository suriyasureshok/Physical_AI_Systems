# Week 2: Latency Distribution & Tail Behavior

## Objective

Experimentally study **latency variability** in a fixed inference workload by running the same computation multiple times and analyzing the resulting latency distribution, focusing on:

- Why latency varies across repeated runs
- How tail latency (p95 / p99) diverges from average latency

This reflects how real AI systems are evaluated in production environments.

### Concepts Explored

This project bridges multiple domains:

| Domain | Concepts Covered |
|:-------|:----------------|
| Statistics | Distributions, percentiles, variance, tail behavior |
| Operating System | System variability, scheduling, context switching |
| Performance Engineering | Latency analysis, tail latency, production metrics |

---

## Experiment Design

### Workload Simulation

We simulate a fixed inference-like workload using the same matrix multiplication operation as Week 1, but with parameters held constant to isolate system-level variability.

### Experimental Parameters

| Parameter | Value |
|:----------|:------|
| **Batch Size** | 32 (fixed) |
| **Sequence Length** | 1024 (fixed) |
| **Embedding Dimension** | 512 (fixed) |
| **Number of Runs** | 100 |

### Metrics Measured

- Latency distribution across multiple runs (milliseconds)
- Statistical measures: mean, median, 95th percentile (p95), 99th percentile (p99)

### Hardware Configuration

All experiments run on **CPU** to highlight system-level variability without GPU-specific optimizations.

---

## Key Observations

### Latency Variability

**Latency shows significant variation** even with identical workloads due to:
- Operating system scheduling overhead
- Memory allocation and garbage collection
- CPU frequency scaling and thermal effects
- Background processes and interrupts

### Tail Latency Divergence

**Tail latency significantly exceeds average latency:**
- p95 latency is typically 15-25% higher than mean
- p99 latency can be 30-40% higher than mean
- This divergence grows with system load and complexity

### Distribution Characteristics

**Latency follows a right-skewed distribution:**
- Most runs cluster around the median
- Occasional outliers create long tails
- Statistical measures (mean vs. median) reveal asymmetry

### System Effects Isolation

**By fixing workload parameters, all observed variation is system-induced:**
- No algorithmic changes between runs
- Highlights the importance of statistical analysis over single measurements
- Demonstrates why production systems monitor percentiles, not just averages

---

## Systems Engineering Insights

>Understanding latency distribution is crucial for:
>- Designing reliable AI systems with SLA guarantees
>- Capacity planning for variable workloads
>- Implementing proper monitoring and alerting
>- Optimizing for tail latency in high-stakes applications
>- Balancing cost vs. performance in production deployments