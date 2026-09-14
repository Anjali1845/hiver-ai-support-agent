# Decision Log

1. Chose Spotify as the target brand because it has abundant historical support conversations.
2. Limited the MVP to 3 intents for consistent manual labeling.
3. Built a manually labeled golden dataset instead of relying on weak labels.
4. Used TF-IDF because it is lightweight, interpretable, and reproducible.
5. Selected Logistic Regression as the baseline intent classifier.
6. Used cosine similarity to retrieve historical Spotify replies.
7. Trained a separate escalation model rather than using fixed rules.
8. Saved all models using Joblib for reproducibility.
9. Evaluated performance using accuracy, precision, recall, F1-score, and a confusion matrix.
10. Accepted lower accuracy and documented limitations instead of overfitting.
11. Kept the pipeline notebook-based so it can be reproduced in under 15 minutes.
12. Prioritized reproducibility over model complexity for the MVP.
