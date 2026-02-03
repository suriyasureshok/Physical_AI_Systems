# 🧠 Wednesday Mini-Project Roadmap (3 Months)

This is a **12-week (≈3 months) Wednesday Mini-Project plan**, designed **specifically for an AI Systems Engineer**, with **gradually increasing complexity** and **zero fluff**.

Each project:
- Is **30–60 minutes**
- Touches **systems + ML + hardware intuition**
- Can live as **one notebook / script per week**
- Is interview-defensible

## Project Checklist

| Status | Week | Mini Project | Focus Area | Estimated Time |
|--------|------|-------------|------------|----------------|
| ✅ | 1 | Embedding Dimension vs Latency & Memory | System Performance Analysis | 30-60 min |
| ✅ | 2 | Latency Distribution & Tail Behavior | Statistical Latency Analysis | 30-60 min |
| ⏳ | 3 | Autograd ON vs OFF: Inference Cost Explosion | PyTorch Autograd Overhead | 30-60 min |
| ⏳ | 4 | Batching vs Throughput vs Latency Trade-off | Throughput-Latency Trade-offs | 30-60 min |
| ⏳ | 5 | Cold Start vs Warm Start Latency | Memory & Cache Warming | 30-60 min |
| ⏳ | 6 | Memory Fragmentation Experiment | Heap Behavior & Fragmentation | 30-60 min |
| ⏳ | 7 | Sequence Length Explosion (Quadratic Effects) | Attention Complexity Scaling | 30-60 min |
| ⏳ | 8 | Concurrency: Single Request vs Multiple Requests | OS Scheduling & Contention | 30-60 min |
| ⏳ | 9 | Admission Control Simulation | Load Shedding & SLO Protection | 30-60 min |
| ⏳ | 10 | Precision Trade-offs: FP32 vs FP16 | Numerical Precision Optimization | 30-60 min |
| ⏳ | 11 | KV Cache Growth Simulator (Conceptual) | State Management in LLMs | 30-60 min |
| ⏳ | 12 | End-to-End Inference Budgeting | System Decomposition & Bottlenecks | 30-60 min |

## Detailed Project Explanations

### Month 1 — Foundations

**Goal:** Stop thinking in "models" and start thinking in **workloads, memory, and latency**.

#### ✅ Week 1: Embedding Dimension vs Latency & Memory

**Objective:** Experimentally study how embedding dimension, batch size, and sequence length affect latency and memory usage in a simplified PyTorch-based inference workload.

**Key Concepts:**
- Linear algebra (vectors, matrix multiplication, dimensionality)
- PyTorch internals (tensor operations, memory management)
- Operating system (memory allocation)
- Statistics (variance, scaling trends)

**Experiment Design:**
- Workload: Random input tensors and matrix multiplication
- Parameters: Batch size (8,16,32,64), Sequence length (512,1024), Embedding dim (128,256,512,1024)
- Metrics: Forward-pass latency (ms), Memory usage (MB)
- Hardware: CPU

**Key Insights:**
- Memory scales linearly with all parameters
- Latency grows non-linearly at higher dimensions
- Batching helps up to a point, then memory pressure dominates
- Sequence length amplifies everything

**Why This Matters:** Essential for capacity planning, hardware choice, and cost optimization in LLM inference.

#### ✅ Week 2: Latency Distribution & Tail Behavior

**Objective:** Study latency variability in a fixed inference workload by analyzing the distribution of latencies across multiple runs, focusing on tail behavior (p95/p99).

**Key Concepts:**
- Statistics (distributions, percentiles, variance, tail behavior)
- Operating system (system variability, scheduling, context switching)
- Performance engineering (latency analysis, tail latency, production metrics)

**Experiment Design:**
- Workload: Fixed matrix multiplication (batch=32, seq=1024, dim=512)
- Parameters: 100 repeated runs
- Metrics: Latency distribution, mean, median, p95, p99
- Hardware: CPU

**Key Insights:**
- Latency varies due to OS scheduling, memory allocation, CPU effects
- Tail latency significantly exceeds average (p95 15-25% higher, p99 30-40% higher)
- Right-skewed distribution with occasional outliers
- All variation is system-induced, not algorithmic

**Why This Matters:** Crucial for designing reliable AI systems with SLA guarantees, capacity planning, and production monitoring.

#### Week 3: Autograd ON vs OFF: Inference Cost Explosion

**Objective:** Compare inference performance with PyTorch autograd enabled vs disabled to understand the overhead of gradient computation.

**Key Concepts:**
- PyTorch autograd (graph construction, backward pass)
- Memory overhead in training vs inference
- Inference optimization techniques

**Mini Project:**
- Run identical inference workload with `torch.no_grad()` and autograd enabled
- Measure latency and memory usage
- Analyze the performance difference

**Why This Matters:** Half of "slow inference" bugs come from forgetting to disable autograd in production.

#### Week 4: Batching vs Throughput vs Latency Trade-off

**Objective:** Explore the fundamental trade-off between batching for throughput vs individual request latency.

**Key Concepts:**
- Throughput (tokens/sec, requests/sec)
- Latency trade-offs
- Queueing theory intuition

**Mini Project:**
- Fix sequence length and embedding dimension
- Sweep batch sizes from 1 to 64
- Measure latency per request and overall throughput
- Plot throughput vs latency curves

**Why This Matters:** Core trade-off in LLM serving systems - balancing user experience with system efficiency.

### Month 2 — Systems Behavior (Real World)

**Goal:** Understand *why systems misbehave under load*.

#### Week 5: Cold Start vs Warm Start Latency

**Objective:** Quantify the performance penalty of cold starts in AI inference systems.

**Key Concepts:**
- Memory allocation patterns
- Cache warming strategies
- Lazy initialization overhead

**Mini Project:**
- Measure latency of first inference run vs subsequent runs
- Quantify the cold-start penalty in milliseconds
- Analyze sources of the delay

**Why This Matters:** Cold starts kill serverless AI systems - understanding this is critical for cloud deployments.

#### Week 6: Memory Fragmentation Experiment

**Objective:** Demonstrate how memory fragmentation affects inference latency over time.

**Key Concepts:**
- Heap allocation behavior
- Memory fragmentation patterns
- Long-running system performance degradation

**Mini Project:**
- Allocate and free tensors of varying sizes in a loop
- Measure latency drift over hundreds of iterations
- Observe how fragmentation increases tail latency

**Why This Matters:** Fragmentation silently increases tail latency in production systems.

#### Week 7: Sequence Length Explosion (Quadratic Effects)

**Objective:** Demonstrate how sequence length creates quadratic scaling effects in attention-based models.

**Key Concepts:**
- Attention mechanism complexity (O(n²))
- Memory growth patterns
- Worst-case scenario amplification

**Mini Project:**
- Fix batch size and embedding dimension
- Sweep sequence lengths from 128 to 4096
- Measure latency and memory scaling
- Plot quadratic growth curves

**Why This Matters:** Explains why long-context LLMs are computationally expensive and hard to serve.

#### Week 8: Concurrency: Single Request vs Multiple Requests

**Objective:** Study how concurrent requests affect individual request latency and system behavior.

**Key Concepts:**
- OS scheduling and thread contention
- Interference between concurrent workloads
- Multi-user system performance

**Mini Project:**
- Run inference in parallel threads/processes
- Compare single request vs concurrent execution
- Measure latency per request and tail behavior
- Analyze interference effects

**Why This Matters:** Production systems handle multiple concurrent requests, not isolated ones.

### Month 3 — AI Systems Thinking (Interview Level)

**Goal:** Design and reason like someone trusted with production systems.

#### Week 9: Admission Control Simulation

**Objective:** Simulate load shedding and admission control to protect system SLOs.

**Key Concepts:**
- Load shedding strategies
- SLO (Service Level Objective) protection
- Backpressure mechanisms

**Mini Project:**
- Artificially overload the system with requests
- Compare accepting all requests vs rejecting beyond a threshold
- Measure p99 latency and system stability

**Why This Matters:** Reliable systems say "no" when overloaded to maintain quality of service.

#### Week 10: Precision Trade-offs: FP32 vs FP16

**Objective:** Compare FP32 vs FP16 precision in terms of performance and accuracy trade-offs.

**Key Concepts:**
- Numerical precision in deep learning
- Approximation techniques
- Memory bandwidth optimization

**Mini Project:**
- Run inference with FP32 and FP16 weights/activations
- Measure latency, memory usage, and throughput
- Discuss conceptual accuracy implications

**Why This Matters:** Precision reduction is a key inference optimization technique in production.

#### Week 11: KV Cache Growth Simulator (Conceptual)

**Objective:** Simulate how KV cache grows with sequence length and concurrency in LLM serving.

**Key Concepts:**
- Key-Value cache state management
- Memory persistence across requests
- Concurrency limits and OOM prevention

**Mini Project:**
- Simulate KV cache size growth with increasing sequence lengths
- Model concurrent request handling
- Estimate maximum concurrency before out-of-memory

**Why This Matters:** KV cache management is fundamental to efficient LLM serving.

#### Week 12: End-to-End Inference Budgeting

**Objective:** Break down end-to-end inference latency into components and identify optimization opportunities.

**Key Concepts:**
- Latency budgeting methodology
- System decomposition
- Bottleneck analysis and prioritization

**Mini Project:**
- Profile inference pipeline components
- Break total latency into: compute, memory transfer, overhead
- Create a latency budget and identify bottlenecks

**Why This Matters:** System design interview gold - decomposing complex systems into optimizable parts.