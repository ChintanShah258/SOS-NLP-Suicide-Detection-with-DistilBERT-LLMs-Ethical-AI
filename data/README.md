# Datasets
This project intends to collect necessary data (for modeling) from a combination of **web scraping** which adheres to ethical considerations as well as **publicly-available datasets**.

## [**Reddit SuicideWatch Posts**](./Reddit_SuicideWatch/)
**Web Scraping**: By launching a web request to Reddit, we load a list of 100 records of posts from `curl https://reddit.com/r/SuicideWatch/new.json?limit=100` which is in the subreddit (i.e., category) named "SuicideWatch". Note that this request could only fetch 100 records at a time. 
Raw data are loaded into `reddit_suicidewatch.json`.

## [**Social Media Sentiments Analysis Dataset**](./Social_Media_Sentiments_Analysis_Dataset/)
Dataset is downloaded into a .csv format from <url>https://www.kaggle.com/datasets/kashishparmar02/social-media-sentiments-analysis-dataset?resource=download</url>.

## [**Twitter Suicidal Data**](./Twitter_Suicidal_Data/)
Dataset is downloaded into a .csv format from <url>https://www.kaggle.com/datasets/hosammhmdali/twitter-suicidal-data</url>.

## [**Depression Tweets**](./Depression_Tweets/)
Dataset is downloaded into a .json format from <url>https://www.kaggle.com/datasets/senapatirajesh/depression-tweets</url>.

# [**Data Processing**](data_processing.py)
Original text is normalized before classification: 
* Removing emojis
* Removing symbols - such as hashtag # sign, the @ symbol, and URLs.
* Removing punctuations
* Converting the entire text to lowercase
* Lemmatization - to replace abstract words with its base form
* Word Tokenization
* Removing Stopwords
* Vectorizing a list of texts - using DistilBertTokenizer since it caters for contextual information within texts.

# Data Splitting
The training set uses data from the following datasets:
* Twitter
* Social Media Sentiment Analysis

The validation set uses data from the following dataset:
* Reddit

The test set uses data from the following dataset:
* Depression Tweet

# Labeling:
We consider a binary classification problem with the following labels and interpretation:
* 0: non-suicidal
* 1: suicidal

* Note: The [data splitting](./data_splitting_DistilBERT.py) and [processing](./data_processing.py) are vectorizing texts using DistilBERT's tokenizer, which is believed to preserve contextual semantic meanings very well. However, by running the scripts `data_processing.py` and `data_splitting_DistilBERT.py` (in sequence), it does not guarantee to work with other types of models like the baseline nor the LLM-based approach. This method is specifically tailored for the 2nd model - fine-tuning a a pre-trained DistilBERT model.
## Text Embedding Vector
**(Title, Post Content, Hashtags)**
* Shape: (n, 3, 768), where n = number of records in a particular set. 
## Metadata Embedding Vector
* Post Category
* Number of Comments
* Hide Score
* Upvote Ratio
* Ups
* Score
* Edited
* no_follow
* over_18
* Created Date / Timestamp
* Country
* Platform
* Sentiment
* Reposts
* Number of Likes