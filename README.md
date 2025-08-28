# 🎮 Steam Games Recommender System – Part 2 (Performance Analysis)

This repository is the **second phase** of the Steam Games Recommender System project.  
While **Part 1** focused on building recommendation models, **Part 2** emphasizes **performance evaluation, comparison, and optimization** of different recommender strategies.

---

## 📑 Project Overview
Recommender systems are essential for guiding players toward games that fit their interests, especially on platforms like **Steam**, which hosts thousands of titles and millions of active users.  

This project evaluates and compares three recommender models developed in Part 1:
- **User-to-User Collaborative Filtering**  
- **Item-to-Item Collaborative Filtering**  
- **Content-Based Filtering (TF-IDF on game titles)**  

The objective of this phase is to:
1. Perform **Exploratory Data Analysis (EDA)** and identify key behavioral patterns.  
2. Evaluate models using both **prediction accuracy metrics** and **ranking-based metrics**.  
3. Compare results, discuss limitations, and propose **future optimization strategies**.  

---

## 📂 Dataset
- Source: **[Steam Video Games Dataset (Steam-200k)](https://www.kaggle.com/datasets/uberkinder/steam-games-dataset)**  
- Files used:
  - `steam-200k.csv` → Raw dataset  
  - `steam_cleaned_normalized_play.csv` → Preprocessed dataset (playtime filtered, normalized, encoded)  
- Records: ~200,000 user-game interactions  
- Features:  
  - `user_id` – unique user identifier  
  - `game_title` – video game title  
  - `behavior_name` – interaction type: `play` or `purchase`  
  - `value` – hours played / purchase flag  
  - `playtime_normalized` – scaled playtime  
  - `user_encoded`, `game_encoded` – numerical encodings for modeling  

---

## 📊 Models Evaluated
- **User-to-User Collaborative Filtering (cosine similarity, KNNBasic)**  
- **Item-to-Item Collaborative Filtering (cosine similarity, KNNBasic)**  
- **Content-Based Filtering (TF-IDF + cosine similarity on game titles)**  

---

## 📈 Evaluation Metrics
The following metrics were used to compare model performance:
- **Prediction Accuracy Metrics**
  - MAE (Mean Absolute Error)  
  - RMSE (Root Mean Squared Error)  
- **Ranking Metrics**
  - Precision@10  
  - MAP (Mean Average Precision)  
  - MRR (Mean Reciprocal Rank)  
  - NDCG (Normalized Discounted Cumulative Gain)  

---

## 🏆 Results Summary
| Model | MAE | RMSE | Precision@10 | MAP | MRR | NDCG |
|-------|-----|------|--------------|-----|-----|------|
| User-to-User CF | 0.0053 | 0.0186 | 0.2533 | 0.9771 | 1.0000 | 1.0000 |
| Item-to-Item CF | 0.0060 | 0.0207 | 0.2533 | 0.9771 | 1.0000 | 1.0000 |
| Content-Based (TF-IDF) | — | — | 0.0288 | 0.0608 | 0.1102 | 0.0911 |

### 🔎 Key Insights
- **Collaborative Filtering (CF)** models — both User-to-User and Item-to-Item — achieved **excellent ranking metrics** (MAP, MRR, NDCG ≈ 1.0).  
- **User-to-User CF** slightly outperformed Item-to-Item CF on **MAE and RMSE**, making it the **best-performing model** in this project.  
- **Item-to-Item CF**, while marginally less accurate, is often **preferred in real-world systems** (like Amazon & Steam) because it scales better for very large datasets.  
- **Content-Based TF-IDF** underperformed since only game titles were available (no genre, tags, or reviews). With richer metadata, its performance would likely improve significantly. 

### ✅ Final Recommendation
- For **accuracy and small-to-medium datasets** → **User-to-User CF** is the best choice.  
- For **scalability and production deployment** → **Item-to-Item CF** is recommended.  
- For **cold-start problems** (new games or new users) → combine CF with **Content-Based** methods in a **hybrid system**.  
---

## 🚀 Future Work
- Fine-tune neighborhood sizes & similarity metrics  
- Add richer metadata (genres, reviews, developers, tags) for content-based methods  
- Incorporate **real-time feedback loops** for adaptive recommendations  
- Explore **deep learning** and **hybrid recommender architectures**  
