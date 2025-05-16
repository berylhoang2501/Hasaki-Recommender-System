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
bash
python content_based/scripts/project2_contentbased_cosinesim_gensim.py
```

Input: Product ID (ma_san_pham).

Output: List of similar products with high cosine similarity scores or Gensim similarity scores.

**Example usage within the script**

```
recommendations = recommend_products_cosine(422211997, df2)
```


