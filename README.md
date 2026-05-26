# Pizza Review Sentiment Analysis

This project focuses on building and optimizing Recurrent Neural Networks (RNNs) to classify the sentiment of pizza reviews. The dataset contains short text reviews in both English and Malay, with original numeric scores that were converted into three sentiment classes (Negative, Neutral, Positive).
What This Project Does

    - Data Cleaning & Exploration: Processes bilingual text data, handles missing or corrupted scores, and analyzes word frequencies and sentence lengths.

    - Data Augmentation: Uses sentence splitting and random word swapping to artificially expand the small training dataset while preserving important sentiment and negation words.

    - Deep Learning Modeling: Builds, trains, and evaluates multiple RNN architectures (SimpleRNN, BiLSTM, and BiGRU) using TensorFlow and Keras to find the best performing text classifier.

Key Decisions Made
1. Moving to 3-Class Sentiment

Instead of trying to predict the exact 0 to 10 score using regression, I grouped the scores into three distinct sentiment categories. This helped the model handle "label noise" where the exact same review text was given different numeric scores by different users.
2. Choosing BiGRU over BiLSTM

I tested a baseline SimpleRNN, a Bidirectional LSTM, and a Bidirectional GRU. I utilized 5-Fold Cross-Validation to ensure the results were reliable. The BiGRU ended up being the best choice because it delivered a highly consistent macro-F1 score across all data splits, outperforming the BiLSTM which had a much wider variance in performance.
3. Custom Embeddings vs. Pretrained (fastText)

I experimented with loading pretrained fastText word embeddings to give the model a head start on understanding English and Malay. However, I found that training a custom embedding layer from scratch actually performed better. The pretrained vectors were likely based on general web text, which didn't transfer perfectly to the highly specific vocabulary of pizza reviews.
4. Careful Data Augmentation

Because the median review length was only 7 words, I avoided aggressive augmentation techniques like random deletion, which could easily erase critical negation words like "didn't" or "tak". Instead, I relied on sentence splitting and random word swapping to force the model to learn context rather than memorizing exact word orders.
