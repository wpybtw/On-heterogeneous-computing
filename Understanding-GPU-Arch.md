# Visualizing Complex Dynamics in Many-Core Accelerator Architectures

## Source

ISPASS'10

http://ieeexplore.ieee.org/document/5452029/

## Problem

GPUs involve massive parallelism at runtime that produces complex dynamic bahaviors. Using performance counter to quantify a entire program might be too general. Consequently, programmers should spend a large amount of effort in finding outstanding metrics related with programs and architectures. 

## Motivation

The need of performance visualization has long been addressed, while there is no open source software that serves to visualize dynamic behavior of CUDA and attribute performance statics to lines of codes.

## Solution

1. Interconnect starvation

Using figures to show dynamic IPC of each SM, comparing between different interconnect strategies.

2. DRAM contention

Using a figure to describe global memory write for each DRAM channel at every cycle.

3. CUDA source

- bank conflict: using a figure to show shared memory access cycles per warp.

- non-coalesced global memory access: showing the number of non-coalesced accesses per line.

- performance bottleneck: showing which lines in the source code were executed during a given period. It is useful even when no performance metrics has been identified.



# Analyzing CUDA Workloads Using a Detailed GPU Simulator

## Source

ISPASS'09

http://ieeexplore.ieee.org/document/4919648

## Problem

GPUs offer order of magnituide computing power more than contemporary CPUs. Thus, understanding GPUs characteristics is vital for improving the performance of parallel applications. This paper run sample applications on a GPU simulator, describing the impact of micro-architectural deisgns.

## Solution

Draw various kinds of figures, such as instruction classification, IPC, occupancy, and speedup to derive performance bottlenecks.

1. Interconnect

Different topology: Butterfly networks, crossbar, 2D torus, ring and mesh, which do not change performance of most benchmarks. The performance is more sensitive to bandwidth than latency.

2. CTA distribution

GPUs launch an abundance of parallel CTA on shader cores. Allowing more CTA running on the same core provides latency benefits, while increasing memory burden and register resource usage.

3. Memory access coalescing

By examine memory utilization and efficiency, we figure out a simple DRAM controller suffers from performance reduction with bank conflicts.

4. Cache

Applications that make extensively use of shared memory do not rely on cache size, while others gain speedup with the growth of cache.


# Demystifying GPU Microarchitecture through Microbenchmarking

## Source

ISPASS'10

http://ieeexplore.ieee.org/document/5452013/

microbenchmark suite: http://www.stuffedcow.net/research/cudabmk

## Problem

GPUs have a different architecture from traditional CPUs. For architecture and compiler developers, it is essential to fully understand detailed of modern GPU designs.

## Solution

1. Cache

Cache way, set, and size could be deduced from repeated and strided access. 

2. Clock values

Clock registers are per-TPC.

3. Arithmetic pipeline

We should test int, float, and double precisions to derive their latency and throughput.

4. Divergence and reconvergence

When threads within a warp diverge, the warp serially executes each path taken from the last program order to the first and then converge. Also, we could set a reconvergence to test whether threads within a warp are executing in a SIMT way or not.

5. Synchronization

__syncthreads only takes effect across multiple warps.

6. Register File

The number of registers used by a thread is rounded to a multiple of four. The number of threads of a block is quantized to a multiple of 64, letting each thread access a logical bank.

7. Cache

Cache has two three main purposes: TLB, data, and instruction. Texture cache has two levels, where the L2-cache is TPC dependent. L1 TLB is fully-associated, holding 16 lines of 512KB TLB line size. Constant and instruction has three cache levels, of which L2 and L3 are unified.

# NVIDIA TESLA V100 GPU ARCHITECTURE

## Source

NVIDIA

http://www.nvidia.com/object/volta-architecture-whitepaper.html

## Features

1. SM

- Tensor cores: eight per SM and two per partition. Each tensor core performs 64 floating-point operation in a cycle, yielding 120 TFLOPS at maximum.

- L0 instruction cache: provide high efficient instruction buffers.

- Unified shared memory and L1 resources: 96KB per SM. Texture units also use L1 cache. It narrows the gap between explict memory and implicit memory.

2. Independent thread scheduling

- Volta maintains per-thread scheduling resources.

- `__syncwarp()` primitive to force reconvergence.

3. MPS

- Provides a hardware-level module that enables MPC clients to submit work to the queue within a GPU.

4. Cooperative groups

- Provides an abstraction by which developers could write flexible codes.


# Understanding the GPU Microarchitecture to Achieve Bare-Metal Performance Tuning

DOI:10.1145/3018743.3018755



More from https://github.com/MattPD/cpplinks/blob/master/comparch.gpu.md