# Structure Based-Hate Speech Detection

Contributors: Ravsimar Singh, Ishita Vohra, Aniket Shrimal, Harsh Shukla

## Problem Statement 
Traditional methods for hate speech detection use tons of training data to mine the hateful structure but due to disproportionate use of different terms they are prone towards learning bias against specific objects, personalities or groups. Idea is to propose a method that takes into account the grammatical structure of the sentence to predict hatefulness.

## Data
We are using already available data on Twitter for hate speech recognition consisting of around 25,000 tweets. Each tweet is classified into 3 categories - Hate speech, Offensive, or neither. We use this information to build a classifier for new tweets.

| Class | No of Tweets  |
| ------- | --- |
| Hate Speech | 1431 |
| Offensive | 19190 |
| Neither | 4163 |

## Preprocessing
We have used the following techniques for preprocessing:
- Stopword Removal - A stop word is a commonly used word (such as “the”, “a”, “an”, “in”). These are usually removed as a part of preprocessing since they do not convey any meaning, but instead, are used to provide fluidity to the sentence.
- Removing excess letters, other twitter specific data (URLs, @mentions, hashtags) - Particularly in social media, these types of words are unique and must be removed, since they do not contribute much to actual meaning being conveyed in the sentence.

## Feature Extraction
Vectorization - We call vectorization the general process of turning a collection of text documents into numerical feature vectors. This specific strategy (tokenization, counting and normalization) is called the Bag of Words or “Bag of n-grams” representation. Documents are described by word occurrences while completely ignoring the relative position information of the words in the document. Scikit-learn provides utilities for the most common ways to extract numerical features from text content, namely:
  * tokenizing strings and giving an integer id for each possible token, for instance by using white-spaces and punctuation as token separators.
  * counting the occurrences of tokens in each document.
  * normalizing and weighting with diminishing importance tokens that occur in the majority of samples/documents.
We used the following features:
* CountVectorizer - It counts the number of times a token shows up in the document and uses this value as its weight.
* TfIdfVectorizer - TF-IDF stands for "term frequency-inverse document frequency", meaning the weight assigned to each token not only depends on its frequency in a document but also how recurrent that term is in the entire corpora.It converts the text documents to a matrix of tfidf features. The combinations of n grams which we used are as follows: 
  * Unigrams
  * Unigrams and Bigrams
  * Unigrams, Bigrams and Trigrams
* POS Tagging - It means labelling words with their Part of Speech. It is a supervised learning solution that uses features like previous word, next word, is first letter captialized etc. NLTK library has a function to get POS tags after tokenization. POS tags unigrams, bigrams and trigrams are weighed by their Tf-Idf.
* Sentiment Analysis + Other features - Sentiment Analysis is an automated process that detects subjective opinions from a text categorising it as positive, negative or neutral. We used Python's NLTK library for this which calculates to polarity(sentiment analysis) of every sentence.Polarity means emotions expressed in a sentence.
* Other Features - We also incorporated various other scores like FRE (Flesh Reading Ease) scores and FKGL (Flesh-Kincaid Grade Level scores) which are based on number of words and syllables in a document. They are used to increase the readability of a document.
* Concatenating the features -  We concatenate these features and make a feature set which is a very high dimensional vector and is sparse. This sparse feature set leads to  overfitting. So to avoid this we use Logistic Regression with regularization parameters (L1, L2).







