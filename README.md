# Hybrid Film Recommender System: Two-Tower Architecture with SVD & PCA
## Project Overview
This project implements a hybrid two-tower recommendation engine designed to tackle the "cold start" problem in recommender systems. By synthesizing user-generated tags with collaborative filtering (SVD) and metadata, the system moves beyond surface-level genre labels to recommend films based on latent thematic alignment.

Using the MovieLens dataset, this project explores how hybrid architectures can improve recommendation quality by combining collaborative filtering with latent structure discovery. It implements and compares PCA and SVD-based approaches, explicitly examining their strengths, limitations, and practical tradeoffs in sparse user–item settings.

## Key Features
Two-Tower Architecture: Separates user preferences and item features into distinct processing pipelines before synthesis.

Latent Semantic Analysis: Utilizes PCA (Principal Component Analysis) to reduce high-dimensional user tags into core thematic components (e.g., distinguishing "Dark Comedy" from "Slapstick" beyond standard genre tags).

Cold-Start Resolution: Implements a fallback strategy using popularity sampling and metadata matching for users with insufficient interaction history.

Matrix Factorization: Applies SVD (Singular Value Decomposition) for robust collaborative filtering on sparse matrices.

## Technical Stack
Language: Python 3.x

Libraries: scikit-learn, pandas, NumPy, UMAP (for visualization), SciPy (sparse matrices)

Data Source: MovieLens Dataset [https://movielens.org/](https://grouplens.org/datasets/movielens/tag-genome-2021)

## Project Context
Developed as a Project for CSCI S-108: Data Mining, Discovery, and Exploration at Harvard Extension School (Harvard DCE).
