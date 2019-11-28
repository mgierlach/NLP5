# Sentiment analysis of political opinions in tweets

I analyzed the sentiment in political opinions of people represented in tweets, using word2vec embedding neural networks for natural language processing problem.

## Introduction

Understanding opinion of people in society about certain political events and knowing their general outlook on the political landscape is crucial, as it allows for knowledge extraction about how they feel about the direction of their country.

Typical polls only answer the most general questions about political party affiliations. They prove to be insufficient in getting to know full distribution of political opinions in diverse societies.

Social media analysis allows us to get insights into what different people think about the political situation. Particularly useful in this context is Twitter, as it is the most advanced social media tool from the linguistic perspective. Tweets can be analyzed from the perspective of sentiment - whether it is positive or negative (some papers also introduce neutral sentiment, I do not take that into account). We can make assumptions that sentiment of a tweet translates author’s opinion about the particular subject he/she is describing.

In my project, I created an early-stage application for the purpose of analyzing people’s opinions about political events, situations and politicians. Application is based on tweets sentiment analysis.

## Methods and experiments

The main obstacle I encountered while working on this project, is the lack of sentiment-labelled tweets databases representing political opinions. Instead of annotating the corpus of political tweets myself, I chose another approach. I build language models on sentiment-annotated text sources, which are not related to politics. I make the assumption that textual opinions exhibiting some sentiment have some general linguistic characteristics that can be applied to politics-themed tweets.

I have taken 2 separate approaches to solving the described problem. First approach is using IMDB reviews dataset (can be found here: http://stanford.edu/~amaas/data/sentiment/). Data in this set are movie reviews with binary classified sentiment labels: 0 - negative sentiment of a review, 1 - positive sentiment of a review. The argument for using this dataset is its large size. The disadvantage is the fact that characteristics of longer movie reviews differ significantly from characteristics of informal political opinions in tweets.

The second approach is building the model based on Sentiment140 dataset (can be found here: http://help.sentiment140.com/home). This set contains opinion tweets regarding brands, products and topics. The advantage of using this dataset is the fact that that tweets have some similar characteristics: informal, short, can be gramatically non-correct. The disadvantage is the fact that these tweets come from distribution of a different theme: opinions about products are usually less emotional, more to-the-point.

Both approaches consist of data processing and building of 2 models. First model in each approach is word2vec embeddings model for high-dimensional word representations that provide the computational method for measuring word similarity. Word2vec model is then used (in both approaches) to create representations for text of tweets, on which I train another binary classification model for sentiment prediction (0 for negative, 1 for positive).

In the end, I use classification models trained on different datasets to classify the sentiment of political tweets coming from The Political Twitter Corpus (can be found here: https://www.usna.edu/Users/cs/nchamber/data/twitter/). I draw 30 tweets from the dataset. Then, I give my personal, by-hand evaluation by logically interpreting tweets from the perspective of sentiment - this is the crucial part as these political tweets are not labelled. After that, I infer both models to get their prediction and compare their outputs to my own evaluation. An approximate accuracy of models at the task of sentiment prediction for political tweets is derived as percentage of correct predictions, when compared with my personal labels.

Python is the language used in the entire project. In both approaches, I use Gensim library for building word2vec models and Random Forest classifier from scikit-learn for building classification predictor. NLTK library is used as an additional tool for tokenization and language processing. The project code generated from Jupyter Notebook is included in this report as an appendix.

## Results
Validation of both models (let’s call them IMDB-trained and Sentiment140- trained) at the stage of testing is not important from the perspective of the final task, which is sentiment prediction of tweets from different distribution. I only perform validations on testing set for word2vec and Random Forest (RF) models for both approaches, so that I do not have an overfitted model.

The real testing is performed on never-seen-before dataset that has been drawed from Political Corpus dataset (described above). After drawing 30 tweets from corpus and personal evaluation of their sentiment, I run the predic- tion models on the tweets and compared them with my own evaluation.

Estimated accuracy of IMDB reviews-trained model: 0.5 (15 correct predictions out of 30).

Estimated accuracy of Sentiment140 tweets-trained model: 0.73 (22 correct predictions out of 30).

## Conclusions
As we can see, the model trained on Twitter data works better. However, since majority of product opinions in that training dataset were negative, it is skewed towards negative classifications. Therefore, there is class imbalance that negatively influences the prediction performance. Majority of political opinions are also negative, therefore limitations of both distributions go together - however products opinions are more negative-skewed than political ones, so the model tends to overestimate the negative sentiment. However, the performance is satisfactory. 73% is quite a good result, when taking into account the fact that we did not train the model on political tweets but on tweets from different distribution. We can conclude that opinions on Twitter have similar characteristics and modeling analysis can be transferred between themes (products and politics).

The model trained on IMDB movie reviews has significantly worse performance. Binary classification with accuracy of 50 % is the same as random drawing - therefore, we can conclude that this approach does not work. Sentiment analysis coming from long text source such as reviews is so different from political-themed tweets that the modeling cannot be transferred between domains.

The Sentiment140-based model could be a good point-of-start for further analysis of people’s political opinions. The model could be improved by getting better annotated data, data coming from politics-related distribution or by using more advanced models, e.g. feedforward neural networks, instead of Random Forest.

### Acknowledgements

The first approach (IMDB-based) to modeling is inspired by a Kaggle kernel of varun08 called ”Sentiment analysis using word2vec”. Some parts of my solution are directly taken from that kernel, other parts are similar, there are some parts where I make my own experimentations.

The second approach (Sentiment140-based) to modeling is heavily inspired by a GitHub repository of Akansha Jain called ”Sentiment-Analysis-Twitter- word2vec-keras”. Some parts of my solution are directly taken from that repository, other parts are similar, there are some parts where I make my own experimentations.
