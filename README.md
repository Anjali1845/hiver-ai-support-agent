# 🎧 Spotify AI Support Agent

An end-to-end NLP project that builds an AI customer support agent for **Spotify** using real Twitter conversations. The system classifies customer messages into intents, retrieves historically grounded Spotify replies, and predicts whether a case should be escalated to a human agent.

## Problem Statement

The objective is to automate Spotify customer support by performing three tasks:

1. **Intent Classification** – Identify the customer's support issue.
2. **Reply Generation** – Retrieve the most relevant historical Spotify support reply.
3. **Escalation Prediction** – Decide whether the conversation should be handled by a human agent.

## Features

* Real Spotify customer support dataset
* 150 manually labelled customer tweets (Golden Set)
* TF-IDF + Logistic Regression intent classifier
* Historical reply retrieval using cosine similarity
* Escalation prediction model
* End-to-end AI support pipeline
* Confusion matrix and classification report evaluation

## Tech Stack

* Python
* Pandas
* Scikit-learn
* TF-IDF Vectorizer
* Logistic Regression
* Matplotlib
* Joblib
* Jupyter Notebook

## Project Structure

```text
hiver-ai-support-agent/
│
├── data/
│   ├── raw/
│   └── golden_set.csv
│
├── notebooks/
│   ├── 01_exploration.ipynb
│   ├── 02_golden_dataset.ipynb
│   ├── 03_train_model.ipynb
│   ├── 04_reply_generation.ipynb
│   ├── 05_support_agent.ipynb
│   └── 06_evaluation.ipynb
│
├── results/
│   ├── confusion_matrix.png
│   ├── intent_model.pkl
│   ├── vectorizer.pkl
│   ├── escalation_model.pkl
│   ├── escalation_vectorizer.pkl
│   ├── reply_vectorizer.pkl
│   ├── reply_matrix.pkl
│   └── reply_pairs.csv
│
├── README.md
├── REPORT.md
├── DECISION_LOG.md
└── requirements.txt
```

## Model Performance

## Model Performance

| Metric | Value |
|---|---:|
| Algorithm | Logistic Regression |
| Vectorizer | TF-IDF |
| Intent Classes | 4 |
| Accuracy | **53.33%** |
| Test Samples | 30 |

The confusion matrix is available in `results/confusion_matrix.png`.

## Evaluation Harness

Generated replies are evaluated using a rubric with four criteria:

* **Relevance** – Does the reply address the customer's issue?
* **Correctness** – Is the suggested action appropriate?
* **Tone** – Does it match SpotifyCares' communication style?
* **Grounding** – Is the reply retrieved from historical Spotify conversations?

## Failure Analysis

| Failure Mode                      | Reason                  |
| --------------------------------- | ----------------------- |
| Premium Billing → General Inquiry | Class imbalance         |
| Login queries                     | Intent overlap          |
| Playback variants                 | Similar vocabulary      |
| Usernames in replies              | Historical Twitter data |
| Small labelled dataset            | Limited generalization  |

## Future Improvements

* Expand the golden dataset to 500+ labelled tweets
* Add additional support intent categories
* Replace TF-IDF retrieval with sentence embeddings
* Remove usernames from retrieved replies automatically
* Deploy the complete system using Streamlit

## Reproducing the Project

```bash
# Clone repository
git clone <your-repo-link>

cd hiver-ai-support-agent

# Create virtual environment
python -m venv venv

# Activate
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

Run the notebooks in numerical order:

1. 01_exploration
2. 02_golden_dataset
3. 03_train_model
4. 04_reply_generation
5. 05_support_agent
6. 06_evaluation
