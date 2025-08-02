# Capstone Project

# Tone Matters: Sentiment Classification of Support Tweets Using VADER and XGBoost

## Overview
This project explores sentiment classification in real-world customer support interactions on Twitter. By combining a rule-based sentiment tool (VADER) with machine learning (XGBoost) and feature extraction (TF-IDF), we built a scalable and interpretable pipeline capable of detecting tone in support tweets. Our goal is to help identify frustrated customers in real time, improve service quality, and monitor trends in support tone at scale.

---

## Dataset
**Source:** [Customer Support on Twitter (Kaggle)](https://www.kaggle.com/datasets/thoughtvector/customer-support-on-twitter)

**Size:** 2.8 million tweets  
**Contents:**

- `tweet_id`

- `author_id`

- `created_at`

- `text` (tweet content)

- `inbound` (customer or company tweet)

- `response_tweet_id`, `in_response_to_tweet_id` (conversation threading)

Note: The response fields were excluded from modeling due to high number of missing values and irrelevance to tone classification.

---

## Methodology

### 1. **Text Preprocessing**

- Removed URLs, mentions, hashtags
- Applied lowercase transformation and stopword removal for TF-IDF
- Cleaned text separately for VADER (sentiment labeling) and TF-IDF (feature extraction)

### 2. **Sentiment Labeling with VADER**

- Tweets labeled as *Positive*, *Neutral*, or *Negative* based on VADER’s compound score thresholds:
  - Positive: ≥ 0.05
  - Neutral: between -0.05 and 0.05
  - Negative: ≤ -0.05

### 3. **Feature Extraction (TF-IDF)**
- Vectorized tweets using unigrams and bigrams (n-gram range: 1–2)
- Max features: 5,000
- Generated a sparse, high-dimensional matrix suitable for XGBoost

### 4. **Modeling with XGBoost**
- Trained on a balanced sample (150k tweets) to address class imbalance
- Applied class weights to improve recall on minority classes (especially Negative)
- Stratified train-test split (80/20)

---

## Results

|Metric      | Value   |
|------------|---------|
|Accuracy    | 77.1%   |
|Precision   | 80.96%  |
|Recall      | 77.1%   |
|F1-Score    | 77.45%  |

**Per-Class F1-Scores:**

- Positive: 0.82  
- Neutral: 0.75  
- Negative: 0.71  

Notably, applying class weights improved Negative recall from 64% to 68%, better identifying frustrated customers.

---

## Visualizations
- Sentiment Distribution Pie Chart
- Inbound vs. Outbound Breakdown
- Word Clouds for Positive, Neutral, and Negative tweets
- Confusion Matrix for model predictions

---

## Key Insights
- Positive tweets made up the majority—often from customers thanking agents or brands using polite templates.
- Negative tweets featured clear emotional language, e.g., “still no response,” “ridiculous,” often paired with punctuation.
- The model was strongest in detecting Positive tone, but tuning for recall greatly improved Negative classification, making it useful for escalation detection.

---

## Business Use Cases
- Real-time sentiment alerts for support supervisors
- Agent performance tracking through tone trends
- Enhancing CRM dashboards with tone-aware insights

---

## Limitations
- Struggles with sarcasm and ambiguous sentiment
- Lack of conversation context (e.g., message threads)
- Static lexicon limits adaptability to new slang or brand-specific language

---

## Future Work
- Integrate context-aware models (e.g., BERT)
- Use metadata features like brand or time of day
- Build a real-time sentiment dashboard
- Expand to multilingual support

---

## Authors
- **Samantha Chickeletti**  
- **Michael Alfrey**  
**Advisor:** Dr. Cohen

---

## License
This project is for academic purposes as part of a graduate capstone in Data Science. Attribution required for any derivative use.


