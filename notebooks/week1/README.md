# Week 1: Embedding Dimension vs Latency & Memory

## Objective

Experimentally study how **embedding dimension**, **batch size**, and **sequence length** affect system performance metrics:

- Latency (milliseconds)
- Memory usage (megabytes)

using a simplified PyTorch-based inference workload.

### Concepts Explored

This project bridges multiple domains:

| Domain | Concepts Covered |
|:-------|:----------------|
| Linear Algebra | Vectors, matrix multiplication, dimensionality |
| PyTorch Internals | Tensor operations, memory management |
| Operating System | Memory allocation, scheduling, cache behavior |
| Statistics | Variance, scaling trends, distribution analysis |

---

## Experiment Design

### Workload Simulation

We simulate an inference-like workload using:
- Random input tensors – Representing embeddings
- Matrix multiplication – Representing linear layers/projections

### Experimental Parameters

| Parameter | Values |
|:----------|:-------|
| **Batch Size** | 8, 16, 32, 64 |
| **Sequence Length** | 512, 1024 |
| **Embedding Dimension** | 128, 256, 512, 1024 |

### Metrics Measured

- Forward-pass latency (milliseconds)
- Approximate memory usage of input tensors (MB)

### Hardware Configuration

All experiments run on **CPU** to highlight raw scaling behavior without GPU-specific optimizations or hardware acceleration.

---

## Key Observations

### Linear Memory Scaling

**Memory usage scales linearly** with:
- Embedding dimension
- Batch size
- Sequence length

**Formula:** `Memory ∝ batch_size × sequence_length × embedding_dim`

### Non-Linear Latency Growth

**Latency grows non-linearly** at higher dimensions due to:
- Increased compute – More FLOPs in matrix multiplication
- Memory bandwidth pressure – Data transfer bottlenecks
- Cache and OS effects – Scheduling and context switching overhead

### Batching Sweet Spot

**Batching helps only up to a point:**
- At **small dimensions** → Batching amortizes compute overhead
- At **large dimensions** → Memory pressure dominates, latency spikes

### Sequence Length Amplification

**Sequence length amplifies everything:**
- Longer sequences exponentially increase memory and compute requirements
- Explains why long-context inference (32K+tokens) is expensive in production
- Critical consideration for LLM deployment at scale

---

## Systems Engineering Insights

>Understanding these scaling behaviors is essential for:
>- Capacity planning for LLM inference
>- Choosing appropriate hardware
>- Setting batch size and context window limits
>- Optimizing cost-per-token in production