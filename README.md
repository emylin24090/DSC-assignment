# **DSC212: Spectral Modularity on the Karate Club Graph**

Name: Emylin Mary Samuval

Roll Number: IMS24090

## Overview

This repository contains my implementation of recursive spectral modularity partitioning on Zachary's Karate Club graph for the DSC212 Graph Theory assignment.

The primary goal is to use the modularity matrix's eigenvectors to find the network's social "fault lines" and to analyze how node-level metrics change as the graph is progressively split.

## Assignment Objectives & Tasks

This project successfully fulfills the following requirements:

Task 1: Recursive Partitioning: Implemented the spectral bipartition algorithm to recursively split the graph until the leading eigenvalue $\lambda_1 \le 0$.

Task 2: Dynamic Visualization: Generated visualizations of the graph after each split, using a fixed layout to make the community evolution easy to follow.

Task 3: Metric Computation: Calculated four key metrics after every iteration: Degree Centrality, Betweenness Centrality, Closeness Centrality, and Clustering Coefficient.

Task 4: Evolution Analysis: Plotted and analyzed how these metrics change for key nodes (e.g., Node 0 and Node 33) as the community structure is refined.

## Files & Outputs

DSC212_Modularity_Assignment.ipynb: The main Jupyter/Colab notebook. It contains all Python code, algorithm implementation, visualizations, and my final analysis.

DSC212__Assignment.pdf: The original PDF handout for the assignment.

README.md: This file.

iter_*.png: (Generated Output) A series of images showing the graph's state after each split.

*_evol.png: (Generated Output) Plots that track the evolution of the four centrality metrics.

metrics_evolution_summary.csv: (Generated Output) A CSV file containing the raw data used for the evolution plots.

## Algorithmic Approach

The community detection algorithm was built from scratch.

Global Modularity Matrix (B): First, the modularity matrix $\mathbf{B}$ is computed for the entire graph. This matrix is defined as $\mathbf{B} = \mathbf{A} - \mathbf{P}$, where $\mathbf{A}$ is the adjacency matrix and $\mathbf{P}$ is the expected connections matrix based on node degrees $k$:

$$\\ B\_{ij} = A\_{ij} - \frac{k\_i k\_j}{2m}$$

Crucially, this uses the original degrees $k$ of all nodes.

Restricted Matrix (B^C): For any community $C$ being evaluated, its restricted matrix $\mathbf{B}^{(C)}$ is found by slicing the global $\mathbf{B}$. This is the key to the method, as it preserves the global degree context.

Spectral Bisection: The leading eigenvalue ($\lambda_1$) and eigenvector ($\mathbf{u}_1$) of $\mathbf{B}^{(C)}$ are calculated.

Splitting Decision: If $\lambda_1 > 0$, the split will increase modularity. The community is thus split into two new groups based on the sign (positive or negative) of the corresponding elements in $\mathbf{u}_1$.

Recursion: The two new sub-communities are placed in a queue for processing. The algorithm halts when no communities can be split further (i.e., when $\lambda_1 \le 0$ for all communities in the queue).

Metric Analysis: At each step, a "fractured" graph is temporarily created (by removing inter-community edges) to correctly calculate how centrality scores are affected by the split.

## How to Run

Clone the repository:

git clone [https://github.com/emylin24090/DSC-assignment.git](https://github.com/emylin24090/DSC-assignment.git)


Install the necessary Python libraries:

pip install networkx numpy matplotlib scipy


Open and run the DSC212_Modularity_Assignment.ipynb notebook. All outputs will be generated in the root directory.

## Key Findings & Results

The algorithm successfully identifies the two primary factions of the Karate Club, centered on "Mr. Hi" (Node 0) and the "Officer" (Node 33).

**The First Split**

The first iteration of the algorithm correctly separates the network into these two main rival groups, validating the method's effectiveness.

Metric Evolution Analysis

Tracking the metrics on the "fractured" graph model provided the most interesting insights:

**Betweenness Centrality**: Drops Dramatically. This was the clearest signal. Global leaders (Nodes 0 & 33) start with maximum betweenness. After the first split, their scores collapse because they are no longer the "gatekeepers" between the two factions.

**Clustering Coefficient**: Generally Increases. As the algorithm isolates dense sub-groups, the local clustering for nodes within those groups rises, indicating a more cohesive (and less "outward-facing") local structure.

**Degree Centrality**: Decreases. In our "fractured" model, nodes lose their "inter-community" links, so their degree centrality (which now only counts in-group friends) naturally drops.

**Closeness Centrality**: Varies. This metric was complex. For many nodes, closeness increased because their average distance to all reachable nodes (i.e., those in their new, smaller community) decreased.
