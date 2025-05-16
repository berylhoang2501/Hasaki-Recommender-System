# Hasaki Recommender System

This project implements a recommender system for Hasaki products, utilizing **Content-Based Filtering** (Cosine Similarity, Gensim) and **Collaborative Filtering** (PySpark ALS, Surprise) to provide personalized product recommendations based on product descriptions and customer ratings.

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Results](#results)
- [License](#license)

## Project Overview
The project is divided into two main approaches:

1. **Content-Based Filtering**:
   - Uses Cosine Similarity and Gensim to recommend products based on textual similarity of product descriptions.
   - Focuses on product metadata (e.g., descriptions) to find similar items.

2. **Collaborative Filtering**:
   - **PySpark ALS**: Implements Alternating Least Squares for large-scale recommendation based on user ratings.
   - **Surprise**: Uses KNNBaseline, SVD, SVDpp, and BaselineOnly models for rating-based recommendations.

**Objectives**:
- Enhance customer experience with personalized product recommendations.
- Compare performance of Content-Based and Collaborative Filtering approaches.

## Dataset
The dataset includes:
- `danh_gia_project2_output.csv`: Customer ratings.
- `san_pham_output.csv`, `San_pham.csv`: Product details.
- `Khach_hang.csv`: Customer information.
- `training_data.csv`, `test_data.csv`: Preprocessed data for Collaborative Filtering.

**Note**: Due to data sensitivity, datasets are not included. 

## Installation
1. Clone the repository:

```
bash
git clone https://github.com/your-username/Hasaki-Recommender-System.git
cd Hasaki-Recommender-System
```

2. Create a virtual environment and install dependencies

```
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

3. Install Java and Spark for PySpark:

Install Java 11.

Download Apache Spark 3.3.0.

Set environment variables:

```
export JAVA_HOME=/path/to/java
export SPARK_HOME=/path/to/spark
export PATH=$PATH:$SPARK_HOME/bin
```

## Usage

### Content-Based Filtering
Run the Content-Based recommender to suggest products based on textual similarity of product descriptions:

```
python content_based/scripts/project2_contentbased_cosinesim_gensim.py
```

Input: Product ID (ma_san_pham).

Output: List of similar products with high cosine similarity scores or Gensim similarity scores.

**Example usage within the script:**

```
recommendations = recommend_products_cosine(422211997, df2)
```

### Collaborative Filtering

1. **PySpark ALS**:
Run the ALS-based recommender to suggest products for a given customer based on their ratings:

```
python collaborative_filtering/scripts/(fixed)pj2_cf(als).py
```

Input: Customer ID (ma_khach_hang).

Output: List of rated products and recommended products with estimated scores.

**Example usage within the script:**

```
rated_products, recommended_products = get_rated_and_recommended_products("567", data_indexed, model, san_pham_file, khach_hang_file)
```

2. **Surprise**:

Run the Surprise-based recommender to train and evaluate models (KNNBaseline, SVD, SVDpp, BaselineOnly) and recommend products:

```
python collaborative_filtering/scripts/(fixed)pj2_cf(surprise).py
```

Input: Customer ID (ma_khach_hang).

Output: List of rated products and recommended products with predicted ratings.

**Example usage within the script:**
```
recommended_products = recommend_products_for_customer(365, training_data, algo, san_pham_df, df_khach_hang)
```

## Streamlit Demo

- Run the Streamlit web application to interact with the recommender system:

```
streamlit run app.py
```

Input: Product ID (ma_san_pham) or Customer ID (ma_khach_hang) via the web interface.

Output: Recommended products based on Content-Based or Collaborative Filtering.

Hosted Demo: Access the live demo at https://recommendation-151224.streamlit.app/.

## Results
### Content-Based Filtering

- Recommends products with high textual similarity (cosine similarity or Gensim similarity scores).
- Effective for products with detailed descriptions.

**Example:** Recommends similar skincare products based on description keywords.

<img width="554" alt="Ảnh màn hình 2025-05-16 lúc 12 49 35" src="https://github.com/user-attachments/assets/44aceb84-7800-4b31-b52f-70cfab58fb8e" />

###  Collaborative Filtering:
- ALS (PySpark): RMSE ~0.85 (varies with preprocessing).
- Surprise: KNNBaseline (optimized) RMSE ~0.80, MAE ~0.65; other models (SVD, SVDpp, BaselineOnly) also evaluated.
- Provides personalized recommendations based on user ratings.

**Example:** Suggests products for a customer based on their purchase history.

<img width="565" alt="Ảnh màn hình 2025-05-16 lúc 12 50 41" src="https://github.com/user-attachments/assets/2b02519d-a825-4a98-a6f9-ccb202920f7f" />

