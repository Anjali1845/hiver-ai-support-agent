# Hiver SDE Intern Take-Home Assignment Report

## 1. Problem Framing

### Objective

The goal of this project is to build an AI-powered Spotify customer support agent using real Twitter conversations. The system should automatically:

- Classify customer messages into support intents.
- Draft replies based on historical Spotify support responses.
- Decide whether the conversation should be escalated to a human agent.

### What “Good” Means

For Spotify, a useful support agent should produce replies that are relevant, consistent with previous support conversations, and able to identify cases that require human intervention such as billing or account issues.

### What I Did Not Build

This MVP intentionally excludes:

- Multi-turn conversation memory
- Sentiment analysis
- Multilingual support
- Generative LLM-based responses

## 2. Dataset

### Primary Dataset

Customer Support on Twitter (Kaggle)

After filtering only Spotify conversations, the project uses real customer tweets together with SpotifyCares replies.

### Golden Evaluation Set

I manually labelled 150 customer tweets into three intent categories and added escalation labels for supervised evaluation.

| Item | Value |
|------|------:|
| Brand | Spotify |
| Manually labelled tweets | 150 |
| Intent classes | 3 |
| Escalation labels | Yes |

## 3. Methodology

The AI support agent is built as a three-stage pipeline.

### Stage 1 — Intent Classification

- TF-IDF Vectorizer
- Logistic Regression
- Input: Customer tweet
- Output: Support intent

### Stage 2 — Reply Retrieval

Historical Spotify support replies are converted into TF-IDF vectors. The system retrieves the most similar customer message using cosine similarity and returns the corresponding Spotify reply.

### Stage 3 — Escalation Prediction

A second Logistic Regression model predicts whether the message should be handled automatically or escalated to a human agent.


## 4. Baselines

| Baseline | Description |
|----------|-------------|
| Trivial | Always predict General Inquiry |
| Simple | TF-IDF + Logistic Regression intent classifier |
| Final | Intent + Reply Retrieval + Escalation pipeline |

## 5. Results

### Intent Classification

| Metric | Value |
|---------|------:|
| Algorithm | Logistic Regression |
| Vectorizer | TF-IDF |
| Accuracy | **36.36%** |
| Classes | 3 |

The confusion matrix shows that General Inquiry is predicted more reliably than Premium Billing because of class imbalance in the training data.

### End-to-End AI Agent

The final system successfully performs three tasks:

1. Predicts the customer intent.
2. Retrieves a grounded historical Spotify reply.
3. Predicts whether escalation is required.


## 6. Evaluation Harness (LLM-as-Judge)

To evaluate generated replies, I designed a simple judging rubric. Each criterion receives a score between 0 and 2, giving a maximum score of 8.

| Criterion | 0 | 1 | 2 |
|---|---|---|---|
| Relevance | Doesn't answer | Partially relevant | Fully addresses the issue |
| Correctness | Incorrect | Partially correct | Correct support action |
| Tone | Poor | Acceptable | Matches SpotifyCares |
| Grounding | Hallucinated | Some overlap | Historical reply based |

### Human vs LLM Agreement

| Customer Message | Human | LLM | Agreement |
|---|---:|---:|---|
| I was charged twice for Premium | 8 | 8 | Yes |
| My music keeps skipping | 7 | 7 | Yes |
| I can't log into my account | 8 | 7 | Partial |

## 7. Failure Analysis

### 1. Premium Billing → General Inquiry

**Example:** “I was charged twice for Premium.”

The classifier predicts General Inquiry because billing examples are underrepresented.

### 2. Login Issues

Short account-related tweets often overlap with General Inquiry, reducing intent precision.

### 3. Retrieved Replies Include Usernames

Historical Twitter replies sometimes contain @mentions that should be anonymized in production.

### 4. Playback Similarity

Different playback bugs use nearly identical vocabulary, making TF-IDF less discriminative.

### 5. Class Imbalance

General Inquiry appears much more frequently than the other classes, reducing recall for minority intents.

## 8. What Is Misleading About My Headline Number?

The headline accuracy of **36.36%** should not be interpreted as production performance.

The evaluation dataset is relatively small, meaning a few incorrect predictions significantly change the overall score. Additionally, the classes are imbalanced, so overall accuracy hides poor recall for minority classes such as Premium Billing.

For this reason, the confusion matrix and per-class precision/recall provide a more meaningful evaluation than accuracy alone.

## 9. Future Work

Given one additional week, I would:

- Expand the golden dataset to 500+ manually labelled tweets.
- Introduce additional support intents.
- Replace TF-IDF retrieval with sentence embeddings.
- Remove usernames from retrieved replies automatically.
- Deploy the complete system as a Streamlit web application.
