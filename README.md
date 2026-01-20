# Hybrid Film Recommender System: Two-Tower Architecture with SVD & PCA
## Project Overview
This project implements a hybrid two-tower recommendation engine designed to tackle the "cold start" problem in recommender systems. By synthesising user-generated tags with collaborative filtering (SVD) and metadata, the system moves beyond surface-level genre labels to recommend films based on latent thematic alignment.

Using the MovieLens dataset, this project explores how hybrid architectures can improve recommendation quality by combining collaborative filtering with latent structure discovery. It implements and compares PCA and SVD-based approaches, explicitly examining their strengths, limitations, and practical tradeoffs in sparse user–item settings.

## Key Features
Two-Tower Architecture: Separates user preferences and item features into distinct processing pipelines before synthesis.

Latent Semantic Analysis: Utilises PCA (Principal Component Analysis) to reduce high-dimensional user tags into core thematic components (e.g., distinguishing "Action Thrillers" from "Critically Acclaimed" beyond standard genre tags).

Cold-Start Resolution: Implements a fallback strategy using popularity sampling and metadata matching for users with insufficient interaction history.

Matrix Factorisation: Applies SVD (Singular Value Decomposition) for robust collaborative filtering on sparse matrices.

## Technical Stack
Language: Python 3.x

Libraries: scikit-learn, pandas, NumPy, UMAP (for visualisation), SciPy (sparse matrices)

### Data Access
**Note:** The dataset used in this project (MovieLens 25M) exceeds GitHub's file size limits.
1. Download the dataset directly from [GroupLens.org](https://grouplens.org/datasets/movielens/25m/).
2. Extract the files into a folder named `data/` in the root directory.
   * Required files: `movies.csv`, `metadata.json`, `ratings.json`, `tagdl.csv`.

### Thematic Discovery via PCA
A core achievement of this project was moving beyond static genre labels. By applying **Principal Component Analysis (PCA)** to user-generated tags, the system identified latent "Mood" clusters.
* **Insight:** Traditional genres (e.g., "Action") are often too broad.
* **Result:** The model identified specific, coherent themes such as *"Critically Acclaimed Dramas"* or *"High-Octane Action"* that cut across genre boundaries.
* **Application:** This allows the recommender to function similarly to Spotify or Netflix, offering "Mood-based" suggestions rather than just category matching.

### Engineering Challenges & Trade-offs
During development, several architectural decisions were weighed against constraints:

* **MinHash & LSH (Locality Sensitive Hashing):**
    * *Attempted:* To account for Actor/Director preferences.
    * *Outcome:* Excluded to prevent bias. While users love "Tarantino films," weighting this too heavily for generic action movies introduced noise.
    
* **Inference Latency vs. Scalability:**
    * *Current State:* Generating top-5 recommendations takes ~20 seconds/user.
    * *Trade-off:* Acceptable for a "Batch Processing" context (updating user towers nightly), but unscalable for real-time serving.
    * *Solution:* Productionising this would require vector indexing tools like **FAISS** or **Annoy** for sub-millisecond similarity search.

* **Explicit vs. Implicit Data:**
    * The model relies on explicit ratings (high user friction). A production iteration would need to weigh implicit signals (watch time, clicks) to reduce the "Cold Start" burden on the user.

### Future Roadmap
* **User Normalisation:** Implement Z-score standardisation on user ratings to account for "Generous" vs. "Critical" rating behaviors.
* **NLP Integration:** Utilise BERT-based embeddings on film Plot Summaries to capture narrative similarity beyond metadata.
* **Scalability:** Migrate the nearest-neighbor search to **FAISS (Facebook AI Similarity Search)**.

## Project Context
Developed as a Project for CSCI S-108: Data Mining, Discovery, and Exploration at Harvard Extension School (Harvard DCE).
