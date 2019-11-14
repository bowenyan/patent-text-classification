# patent-text-classification

We provide a technology intelligence platform for companies, to analyse their competitors, explore their own technology road map, build technology opportunities, using patent data. However, for SMEs, starups, they might not have patents. Therefore, to classify unstructured technology data for building technology portoflio is very important in real business situations.

In the experiments, we only use very small samples to test/select text classification methods, with less computation time required for training. The process is to get some ideas of preparing data, selecting suitable classifiers, etc.

## Dataset:

Download the dataset from https://github.com/JasonHoou/USPTO-2M

## Data preprocessing: 

1. Remove invalid class information from the original dataset. Most of those invalid classes have only one patent.
2. Create balanced dataset for each class. 


## Feature representation:

1. Use own vocabulary to build feature matrix, according to the domain knowledge of the dataset. The vocabulary contains n-gram words, generated by using spaCy, Textblob, etc.

    - tf-idf vectorization.
    
    - tf-idf vectorization with feature selection (5k~20k features).
    
2. Word embeddings. 
    
    - Train word embedding model using Skip-gram model based on patent abstracts. Plot some cases using t-SNE and PCA.
    
    - Allow neural networks to learn the embedding layer itself.

## Classifiers:

1. Traditional methods, like Naive Bayes, SVM, Logistic regression.

2. Neural networks, like ANN, CNN, LSTM, etc. 
    - The embedding layer: use pre-trained word embeddings or allow to learn the word embedding itself.
    
    - Hidden layers: Relu as the activation function.
    
    - Output layer: Softmax (multiple-class classification problem) as the activation function, categorical cross-entropy as the loss function.

## Some findings:

1. Since we only used patent abstracts for testing, the results of using “bag of words” and “word embedding“ seem not very different. It may also because the technical words used in patent documents are more important for choosing patent classes. Sequence representation of words in patent documents might not affect the classification very much.

2. In the experiments of using neural networks, 1 hidden layer performs well, compared to 2 or 3 hidden layers.

3. Simple multi-layer perceptron model takes n-grams as input perform good even with smaller samples, compared to SVM, Naive Bayes.

## Future work:

1. Use the entire patent dataset (6M+ patents from 1976 to 2019), descriptions of patent documents as texts, and different classification systems (e.g., Cooperative patent classification, WIPO technology fields).

2. Test different variations, e.g., seqCNN, seq2seq with attention, bidirectional RCNN.

3. Train doc2vec based on patent abstracts and descriptions.

4. Use different pre-trained word2vec models from Google and Stanford.

5. Use grid search, k-fold cross-validation to optimize hyperparameters.

