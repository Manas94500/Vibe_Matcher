# 🚀 Vibe Matcher: A Semantic Search Recommendation System
This project is a Google Colab notebook that prototypes a "Vibe Matcher" recommendation system. Instead of relying on rigid tags or keyword search, this system uses **semantic search** to understand the *intent* and *feeling* behind a user's text query (e.g., "energetic urban chic").

It then finds the top-matching products from a sample catalog based on this "vibe" using vector embeddings and cosine similarity.

## ⚡ Quick Demo

The core idea is to translate abstract feelings into concrete products:

**User Vibe:** `"something cozy for a cold day"`
⬇️
**Embedding Model:** `[0.01, 0.4, -0.2, ...]`
⬇️
**Vector Search:** Finds closest product vector
⬇️
**Top Match:** `"Cozy Knit Sweater"` (Similarity: 0.85)

## ✨ Features

* **Semantic Search:** Understands the *meaning* of a query, not just the keywords.
* **Top-K Matches:** Returns the top 3 most similar products.
* **No Match Fallback:** Gracefully handles queries that don't match any products (based on a similarity threshold).
* **Local & Free:** Uses the `sentence-transformers` library, so it runs 100% free in Colab with no API keys required.
* **Performance Metrics:** Includes a simple test to plot the search latency.

## ⚙️ How It Works

This prototype follows a simple vector search pipeline:



1.  **Data Prep:** A sample catalog of 7 fashion products is created in a Pandas DataFrame.
2.  **Embedding:** A pre-trained `SentenceTransformer` model (`all-MiniLM-L6-v2`) converts all product descriptions into numerical vectors (embeddings).
3.  **Query:** A user's text query (e.g., "edgy and futuristic") is converted into a vector using the *same* model.
4.  **Search:** The query vector is compared against all product vectors using **Cosine Similarity** from `scikit-learn`.
5.  **Ranking:** The system sorts the products by their similarity score and returns the top 3 matches.

## 🛠️ Tech Stack

* **Language:** Python
* **Notebook:** Google Colab
* **Data:** Pandas
* **Embeddings:** `sentence-transformers` (`all-MiniLM-L6-v2`)
* **Vector Math:** `scikit-learn` & `numpy`
* **Plotting:** `matplotlib`

## 🏃 How to Run

1.  Click the "Open in Colab" badge at the top of this README.
2.  In the Colab notebook, click **Runtime** > **Run all**.
3.  The notebook will install all required libraries and run the code from top to bottom.
4.  You can see the output for the test queries at the bottom, or add your own query in the test cells!

## 💡 Reflection & Future Improvements

* **Scalability:** The current brute-force search is $O(N)$ and won't scale. The clear next step is integrating a dedicated vector database (e.g., **Pinecone, Chroma, or Faiss**) to use Approximate Nearest Neighbor (ANN) search for $O(\log N)$ or $O(1)$ lookup.
* **Data Quality:** The system is only as good as the product descriptions. A real-world version would need a robust data pipeline.
* **Hybrid Search:** This prototype only uses vector search. A production-grade system would combine this with keyword search (BM25) and metadata filtering (e.g., "price < $50", "category == 'jackets'") for more powerful, relevant results.
