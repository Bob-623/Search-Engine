# New insights from ‘old news’: Repurposing Reuters text classification datasets for IR use with LLM annotation
**AUTHORS: KAREN KIERNAN (‘KAREN’), DINGKAI GUO (‘BOB’), MENGYU LI (‘LI’) (GROUP 27)**

## Introduction 
Group 27 on the QMUL Information Retrieval module (ECS736P) constructed a **search engine** for the group assignment Semester B. The project
repurposed a famous but old text classification dataset, the **Reuters-21578**, as a fully annotated 
Information Retrieval dataset. This was achieved by using an LLM for relevance annotation.

**BM25 vs BM25F**

BM25 remains an industry standard as a first pass key word matching filter, and is a component of larger 
search engines. The Reuters dataset has a structured text format e.g. article body and article title. This 
allows us to explore the use of BM25F in comparison with BM25.

**LLM relevance score labels**

We used ChatGPT to generate relevance scores for the Reuters 21578 dataset for the given set of 
queries. This served as the ‘ground truth’ of document relevance rankings. 

## Repository Structure



![image](https://github.com/user-attachments/assets/48915f9c-7aac-4323-8194-b9594159e81e)



## Tools used to develop search engine
The main tools used were:
* General programming: Python – main language for calling wide variety of libraries.
* Pre-processing: NLTK (stop word removal, tokenization, lowercase)
* Search engine: PyTerrier. We chose it because PyTerrier is flexible for BM25 and BM25F.
* Golden Standard LLM: ChatGPT

## Pipeline steps
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

<center>

| Query   |      Text      |
|----------|:-------------:|
| Q1 |    "Impact of interest rate hikes on stock market"   |
| Q2 | "Government policies affecting technology investments" |
| Q3 |  "Gold rush of the digital age"|
| Q4 |  "International geopolitical tensions" |
| Q5 |    "The rise of computer power"   |
| Q6 |    "War"   |
| Q7 |    "Japan"   |
| Q8 |    "Merrill Lynch"   |
| Q9 |    "Tariffs"   |
| Q10 |    "Morgan Stanley"   |



</center>



### Step 5. Evaluate performance of BM25 and BM25F vs golden standard

The most appropriate metric for comparing rankings is Normalized Discounted Cumulative Gain 
(nDCG@k). This metric is used to evaluate the performance of each model compared to the 
control benchmark of ChatGPT rankings, at k= 10 to 50 in increments of 10.
