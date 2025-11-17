# DSC212 – Modularity on the Karate Club Graph

Name: Emylin Mary Samuval
Roll Number: IMS24090

This repository contains my implementation of recursive spectral modularity partitioning on the Zachary Karate Club graph for the DSC212 Graph Theory assignment.

## Overview

The goal of the assignment is to detect multiple communities using modularity-based spectral splitting and to study how different node-level metrics behave across the recursive partitions.

### What the notebook includes

*  Construction of the Karate Club graph

*  Modularity matrix computation

*  Recursive spectral bisection for community detection

*  Graph visualisation after each split using a fixed layout

*  Centrality and clustering measures:

*  Degree centrality

*  Betweenness centrality

*  Closeness centrality

*  Clustering coefficient

*  Plots showing how these metrics behave across iterations

*  Generated Outputs

## Mathematical Methodology

The core of the analysis relies on the **Modularity Matrix $B$**, defined as the difference between the actual adjacency matrix $A$ and a null model based on degree distribution:

$$B_{ij} = A_{ij} - \\frac{k_i k_j}{2m}$$

### The Recursive Algorithm:
1.  **Construct $B^{(C)}$:** Form the modularity matrix for the current community $C$.
2.  **Eigen-Decomposition:** Solve for the leading eigenpair $(\lambda_1, u_1)$.
3.  **Check Modularity Gain:**
    * If $\lambda_1 > 0$: Split community $C$ into two groups based on the signs of elements in $u_1$.
    * If $\lambda_1 \le 0$: Stop; the community is indivisible.
4.  **Recurse:** Apply steps 1-3 to all resulting subgroups.

### Running the notebook generates:

*  Community visualisation images (iter_0.png, iter_1.png, …)

*  Metric evolution plots (deg_evol.png, bet_evol.png, clo_evol.png, clu_evol.png)

*  metrics_evolution_summary.csv summarising all computed metrics

All output files are saved in the root of this repository.

### Discussion Summary

Nodes like 0 and 33 remain central throughout the recursive splits because they act as major hubs connecting different parts of the graph. Their degree stays the highest since the network structure itself doesn’t change, only the way we group nodes into communities changes. Betweenness centrality highlights nodes that lie between two communities, so these nodes continue to have high values as the algorithm separates the graph. Closeness centrality also reflects this, since central nodes still have shorter paths to the rest of the graph. The clustering coefficient is higher for nodes that belong to tightly connected subgroups, and lower for nodes at the boundaries of the splits. Overall, the community structure mainly reveals which nodes are internal to a community and which ones act as bridges between groups.

### How to run

Open the notebook

Run all cells top to bottom

All plots and CSV files will appear in the same directory
