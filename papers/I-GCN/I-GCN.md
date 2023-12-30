# I-GCN: A Graph Convolutional Network Accelerator with Runtime Locality Enhancement through Islandization

《I-GCN：通过岛屿化增强运行时局部性的图卷积网络加速器》

## INTRODUCTION

GCN加速的两种主要方式：  

1. PULL-based aggregation(HyGCN)
   ![pull-based](images/pull-based.png)
   特征矩阵需要多次访问
2. PUSH-based aggregation(AWB-GCN)
   未解决结果矩阵不规则和随机访问的问题

解决方案——“岛屿化”

