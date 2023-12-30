# HyGCN: A GCN Accelerator with Hybrid Architecture

- MLP - multi layer perceptron
- MVM - matrixvector multiplication
- PM - programming model

## Architecture Overview

1. To hide the DRAM access latency, both the Edge Buffer and Input Bufferadopt the **double buffer technique**.
2. Different from normal **systolic array**, our systolic array is **multi-granular(多粒度，有两个模式)** that can be used as **multiple smaller arrays** or **a whole large array** under different optimization scenarios.
3. To improve the bandwidth utilization, a **prefetcher** is designed to explicitly prefetch graph data and parameter data.

![架构图](images/HyGCN_no1.png)

## Aggregation Engine

1. Execution Mode
   1. vertex-concentrated

        每个SIMD核心处理一个节点

   2. vertex-disperse

        每个SIMD核心处理一个特
        - all cores are always busy
        - intra-vertex parallelism, the vertex latency is smaller
        - enable the immediate processing of each vertex in the following Combination Engine

        ![运算模式](images/HyGCN_no2.png)

2. Graph Partitioning (Static)

    ![特征矩阵分区](images/HyGCN_no3.png)

    ![分区聚合](images/HyGCN_no4.png)

3. Data-Aware Sparsity Elimination (Dynamic)

    Window Sliding, Window Shrinking

    ![窗口应用](images/HyGCN_no5.png)

    ![窗口聚合](images/HyGCN_no6.png)

## Combination Engine

![多重脉动阵列](images/HyGCN_no7.png)

1. Cooperative Working Mode(vertex-concentrated)

    ![合作模式](images/HyGCN_no8.png)

2. Independent Working Mode(vertex-disperse)

    ![单独模式](images/HyGCN_no9.png)

## Inter-Engine Optimization

1. Latency- or Energy-Aware Pipeline

    ![Latency- or Energy-Aware Pipeline](images/HyGCN_no10.png)

2. Coordination of Off-chip Memory Access

    ![Coordination of Off-chip Memory Access](images/HyGCN_no11.png)
