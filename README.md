<h1 align="center">IAC Project - K-Means Clustering</h1>

## Project Overview

This repository contains the implementation of a k-means clustering algorithm developed for the IAC (Introdução à Arquitetura de Computadores) course @IST Instituto Superior Técnico (2023/2024). The project focuses on identifying clusters of points in a two-dimensional space using RISC-V assembly language.

### 📁 Project Details
- **Goal**: Develop a program in RISC-V assembly that identifies $ k $ groups of points based on their relative proximity in a 2D space using the k-means algorithm.

### Key Features
- **Inputs**:
  - `points`: An array of points in 2D space (each point consists of a pair of coordinates, {x, y}).
  - `n`: The number of points, representing the dimension of the `points` array.
  - `k`: The number of clusters to consider.
  - `l`: The maximum number of iterations for the algorithm.

- **Output**: The program displays the $ k $ clusters and their respective centroids on a 2D LED matrix screen, updating the display with each iteration.

## Project Organization

The project is designed to be completed in groups of three students. It is divided into a set of problems, each solved by a procedure (or function). It is recommended that each group implements and tests each procedure before moving on to the next, allowing for gradual progress toward the final solution.

### Procedures
- **cleanScreen**: Clears all points from the screen.
- **printClusters**: Displays the points on the screen, coloring them according to their assigned clusters.
- **printCentroids**: Displays the centroids of the clusters on the screen.
- **calculateCentroids**: Computes the centroids based on the current cluster assignments.
- **mainSingleCluster**: Executes the main procedure for the preliminary submission, performing the steps to display the initial points and centroids.

## Implementation Details

- The project must be developed using the Ripes simulator, focusing on a 32-bit RISC-V processor.
- All calculations must use integer values, avoiding floating-point operations.
- The algorithm is designed to run a single instance of k-means, updating the display with the current state after each iteration.

## Tools and Technologies

- **RISC-V Assembly**: For low-level programming and algorithm implementation.
- **Ripes Simulator**: For simulating the RISC-V architecture and visualizing the output on a LED matrix.

## Notes

- A good understanding of the k-means algorithm is essential for effective implementation. For more information, refer to [StatQuest's K-Means Clustering](https://statquest.org/statquest-k-means-clustering/).

