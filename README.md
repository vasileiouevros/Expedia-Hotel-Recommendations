# Expedia Session-Based Hotel Recommender

## 📌 Overview

This project implements a session-based recommendation system using the Expedia dataset.
The goal is to predict the next hotel a user is likely to click based on their current browsing session.

The approach uses **Word2Vec embeddings** to model relationships between hotels from click sequences.

---

## 🧠 Problem Definition

Users browse multiple hotels within a session, and their preferences can change dynamically.
This project formulates recommendation as a **next-item prediction task** using sequential interaction data.

---

## 📊 Dataset

* Source: [Expedia PKDD 2022 Dataset](https://github.com/ExpediaGroup/pkdd22-challenge-expediagroup/releases)
* Each session is a sequence of hotel IDs
* Preprocessing steps:

  * Convert click strings → ordered sequences
  * Remove sessions with < 2 interactions
  * Sample 5% of data for feasibility
  * Split into:

    * 80% training
    * 10% validation
    * 10% test

---

## ⚙️ Methodology

### Word2Vec Modeling

* Sessions → sentences
* Hotels → words
* Model: Skip-gram with negative sampling

### Best Configuration

* vector_size = 64
* window = 3
* negative = 8
* alpha = 0.01
* min_count = 5
* epochs = 10

---

## 🔍 Recommendation Strategies

1. **Popularity Baseline**

   * Rank hotels by frequency

2. **Previous-Item Model**

   * Use last clicked hotel as query

3. **Context-Based Model**

   * Average all previous hotel embeddings

---

## 📏 Evaluation

* Metric: **Hits@10**
* Task: Predict final click in each session
* Input: all previous clicks
* Note: Sessions with missing embeddings are skipped

---

## 📈 Results

| Model            | Hits@10 |
| ---------------- | ------- |
| Popular baseline | 0.0035  |
| Previous-item    | 0.0592  |
| Context-based    | 0.0405  |

👉 Embedding-based models significantly outperform the baseline.
👉 The **previous-item model performs best**, highlighting the importance of recent interactions.

---

## 💡 Key Insights

* Sequential behavior improves recommendations
* Recent interactions carry the strongest signal
* Data sparsity remains a major challenge

---

## ⚠️ Limitations

* Sparse data affects rare hotels
* Word2Vec cannot model long-range dependencies
* Some sessions are skipped due to missing embeddings

---

## 🚀 Future Work

* Try RNNs / Transformers
* Add hotel metadata (price, location)
* Use additional metrics (MRR, NDCG)

---

## 🛠️ Tech Stack

- Python  
- Pandas, NumPy (data processing)  
- Matplotlib, Seaborn (visualization)  
- Scikit-learn (data splitting)  
- Gensim (Word2Vec embeddings)

---

## 📂 Project Structure

```
├── Expedia Hotel Recommendations - Code.ipynb
├── Expedia Hotel Recommendations - Report.pdf
├── README.md
```

---

## 👤 Author

Evros Vasileiou
University of Nicosia
