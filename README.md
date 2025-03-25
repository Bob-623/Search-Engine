# New insights from ‘old news’: Repurposing Reuters text classification datasets for IR use with LLM annotation
**AUTHORS: KAREN KIERNAN (‘KAREN’), DINGKAI GUO (‘BOB’), MENGYU LI (‘LI’) (GROUP 27)**

## Introduction 
This report outlines a review of literature on search engine design and proposes an architecture for 
repurposing a famous but old text classification dataset, the Reuters 21578, as a fully annotated 
Information Retrieval dataset. This will be achieved by taking advantage of the recent trend in using an 
LLM for relevance annotation of large datasets.

## Files: Datasets and jupyter notebooks
 - EXPLAIN THE FILE STRUCTURE IN THE REPOSITORY HERE


## BM25 vs BM25F
BM25 remains an industry standard as a first pass key word matching filter, and is a component of larger 
search engines. The Reuters dataset has a structured text format e.g. article body and article title. This 
allows us to explore the use of BM25F in comparison with BM25.

## LLM relevance score labels
We used ChatGPT to generate relevance scores for the Reuters 21578 dataset for the given set of 
queries. This served as the ‘ground truth’ of document relevance rankings. 

## Tools used to develop search engine
A variety of tools will be used at each stage, subject to evaluation during the implementation phase. The 
main tools we are likely to use are:
* General programming: Python – main language for calling wide variety of libraries.
* Pre-processing: SkLearn , NLTK, SpaCy – NLP libraries.
* Search engine: PyTerrier. We have chosen it because PyTerrier is flexible for BM25 and BM25F.
* Golden Standard LLM: ChatGPT/Bert. ChatGPT is a widely used commercial standard. BERT is widely 
used for information retrieval. A decision will be made during implementation.
* OPTIONAL: Embedding: If this option is exercised then word embedding libraries such as GloVe will be used


### Step 1: Data Preprocessing
The goal of data preprocessing is to clean and standardize data to facilitate efficient indexing and 
improve search quality. Preprocessing steps included: Text Normalization, Tokenization, Stopword Removal, Stemming and Lemmatization, Term Frequency (TF) Calculation

### Step 2: Indexing
The inverted index is the core data structure in search engines. It efficiently stores term-document 
relationships to speed up searches and eliminate the need to scan all documents.

### Step 3: Ranking with BM25/BM25F
Run the test set of queries separately using two routes: BM25 and BM25F. BM25F weightings applied to the article title (1) and article body (0.5).


### Step 4. Use an LLM to create a ‘golden standard’ ranking of documents
ChatGPT was used to assign a 1-5 relevance score to all documents in dataset for each test query. These are:

"Bank profit report for Q4",                               # Q1
"Impact of interest rate hikes on stock market",           # Q2
"Government policies affecting technology investments",    # Q3
"Gold rush of the digital age",                            # Q4
"Taylor Swift global tour",  # Assume no results           # Q5
"Climate Change Crisis",      # Assume a few results       # Q6
"International geopolitical tensions",                     # Q7
"The rise of computer power"                               # Q8
"The President of the United States",                      # Q9
"War"                                                      # Q10


### Step 5. Evaluate performance of BM25 and BM25F vs golden standard
3. The most appropriate metric for comparing rankings is Normalized Discounted Cumulative Gain 
(nDCG@k). This metric is used to evaluate the performance of each model compared to the 
control benchmark of ChatGPT rankings, at k= 10 to 50 in increments of 10.
