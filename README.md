# 🎧 Spotify AI Support Agent

An NLP project that classifies Spotify customer support tweets into support intents using TF-IDF and Logistic Regression.

## Features

- Cleaned real Spotify support tweets
- Manually labeled 50 tweets into 3 intents
- TF-IDF text vectorization
- Logistic Regression classifier
- Confusion Matrix evaluation
- Saved trained model for inference

## Tech Stack

- Python
- Pandas
- Scikit-learn
- TF-IDF
- Logistic Regression
- Matplotlib
- Jupyter Notebook

## Project Structure

data/
├── raw/
├── golden_set.csv

notebooks/
├── 01_exploration.ipynb
├── 02_golden_dataset.ipynb
├── 03_train_model.ipynb

results/
├── confusion_matrix.png
├── intent_model.pkl

## Model Performance

- Algorithm: Logistic Regression
- Vectorizer: TF-IDF
- Training Samples: 50 tweets
- Classes: General Inquiry, Playback Issues, Premium Billing
- Accuracy: **36.36%**

## Future Improvements

- Increase labeled dataset to 500+ tweets
- Add more intent categories
- Deploy as a Streamlit web application