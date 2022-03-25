
# EMFoS

**EMFoS: Evaluation Metrics For Summarization** 

Measuring the performance of NLP tasks like News Summarization is a very challenging task. It's not always possible to have human annotators review it. We need an "Automatic Evaluation Metric" that can work without human intervention. It may not be as good as human ratings but it can be a "**proxy**". Thus, a good "Automatic Evaluation Metric" is supposed to be a good "Proxy" of Human Evaluation (or Ratings). The idea is that if we have multiple options for evaluation metrics, we choose one which is a better proxy of human evaluation compared to others.  

This Repository explores various evaluation metrics, including de-facto-evaluation-metric-for-summarization "ROUGE Score" and some contextual-similarity-based metrics. 

We compute Pearson and Spearman-Rank correlation between a respective evaluation metric and human ratings to know "how good proxy the given metric is of human ratings?"

**PS:** We get results supporting the fact that contextual similarity is a better proxy of human ratings than ROUGE Score. 
## Motivation

Evaluation Metrics like [ROUGE Score](https://aclanthology.org/W04-1013/), which only considers the n-gram overlap between candidate and gold standard, can wrongly penalize abstractive summaries that may not have significant n-gram overlap with a gold standard but convey the same meaning.

**Example:** 

- **Reference:** The weather is cold today.
- **candidate:** It's freezing today. 

As you can see in above above example, referene and candidate have very little n-gram(n=1,2,3..) overlap but are conveying the same thing. 

The above example consisted of only one sentence, but our summaries may contain many. While evaluating the summary, one should look for qualitative measures like 
- **Grammatical correctness** 
- **Arrangement of sentences** 
- **Text Quality** (Quality of language used and suitability with a set of users the application is serving to)
- **Coherence** (Conciseness and Exhaustiveness)

An ideal automatic evaluation metric should consider the above points rather than just computing n-gram overlap.  


## Methodology

Once the motivation was clear and the path-to-be-explored was decided (i.e., to find an automatic evaluation metric that has a high correlation with the qualitative measures), we started looking for a relevant dataset, but we found none. 

### Dataset Building

We decided to take the [Indian News Dataset](https://www.kaggle.com/datasets/sunnysai12345/news-summary), a collection of news articles, news titles, and their respective human-written summaries scraped from [Inshorts](https://www.inshorts.com/).

we did some pre-processing on the above mentioned dataset and took a sample of 1001 tuples and generated abstractive summaries using [bart-large-cnn](https://huggingface.co/facebook/bart-large-cnn). we used in-house [django-based tool](https://github.com/TarangRanpara/SummaryAnnotatorTool) for collecting human ratings. 

We asked our reviewers to rate given summary between [1-5] on following points. 

-  Grammatical Correctness
-  Arrangement of sentences/Flow of information
-  Text Quality
-  Conciseness
-  Exhaustiveness
-  Overall Rating (subjective to the annotator)

Since the ratings can be subjective to a reviewers's understanding, we collected two sets of ratings for same set of summaries from **two distinct** set of reviewers. 

More information about the dataset can be found [here](https://github.com/TarangRanpara/EMFoS/blob/main/Dataset/README.md). 
        

### Computing correlation

Once the human ratings were collected, it was now time to build a score out of it and measure its correlation with candidate evaluation metrics.  

For building a score out of human judgments, we first averaged the scores from both set of annotations to counter the subjectivity of opinions.

From the collected human judgments, we computed two kinds of scores. 

- **Score-1:** Used "Overall Rating" Score directly (also called "OVERALL SCORE")
- **Score-2:** took a Weighted average of qualitative measures (except "Overall Rating") listed above (also called "WEIGHTED SCORE"). more on this, [here](https://github.com/TarangRanpara/EMFoS/blob/main/Notebooks/README.md). 

we then computed correlation of score-1 and score-2 with set of candidate evaluation metrics falling broadly into 3 categories. 

- **N-Gram Overlap**
    
    [ROUGE Score](https://aclanthology.org/W04-1013/) measures n-gram overlap between candidate and gold standard summary. 

    we have considered ROUGE-1, ROUGE-2 and ROUGE-L.  
- **Contextual Similarity** 

    We computed cosine similarity of document embeddings of candidate and gold standard for measuring contextual similarity. 


    For computing document embeddings, we used **four** different varieties of methods. 
    
    | Type of model      | Description |
    | :---        | :--- |
    | Gensim based models |Computes average of word embeddings to get document embeddings.|
    | Spacy Models | Directly used in-built functionality to get the document embeddings. |
    | Vanilla Transformers (with Bert-like architecture) | Computed embeddings of [CLS] token, which is generally found at the very beginning of the document.  |
    | Sentence-transformers | Directly used in-built functionality to get the document embeddings.|

- **Pairwise Contextual Similarity** 
    
    we experimented by using different models in [BertScore](https://github.com/Tiiiger/bert_score). 
    
    ![BertScore](/Assets/bert_score.png)
   

more about these metrics can be found [here](/Notebooks/README.md). 
## Repository Structure

- **Notebooks** directory contains code for computing different scores and computing their correlation with human judgements.
- **Dataset** directory contains the dataset. 
- **Assets** directory contains the images/assets used in this repository.    

```
EMFoS
|
│   README.md  
│
└───Notebooks 
│   │   ComputePearsonCorrelation.ipynb
│   │   ComputeSpearmanCorrelation.ipynb
|   |   ComputeScores.ipynb
|   |   README.md
│   
└───Dataset
|   │   DATA.csv
|   │   README.md
|
───Assets  
│   │   ..
|   |   ..
|   |   README.md
|
```

## Results 

Detailed comparison of various evaluation metrics with human judgment with Significance testing can be found [here](https://docs.google.com/spreadsheets/d/1FdVI9LMi-UzOSfdZsdJBWsNYFlnYwAIJBZ5JVgewgvo/edit?usp=sharing). 


## Acknowledgements

I want to convey special gratitude to my colleagues and friends who contributed to the rating process. It wouldn't have been possible without your support.  

People who contributed to building the dataset by rating the machine-generated summaries:
 - [Darshil Patel]()
 - [Prahar Pandya]()
 - [Dhyanil Mehta]()
 - [Devansh Choudaha]()
 - [Kishan Vaishnani]()
 - [Tarang Ranpara]()
 - [Shradha Makhija]()
 - [E.V.V. Haricharan]()
 - [Sana Baid]()
 - [kaushal pandya]()
 - [Dev Dave]()
 - [khushali Ratanghayara]()
 - [Harsh Bhatt]()
 - [Ravi Dave]()
 - [Mihir Kotecha]()
 - [Raj Shah]()
 - [Vikas Gajera]()
 - [Jainil Soni]()
 - [Kevin Jadia]()
 - [Jugal Soni]()
 - [Jilsa Chandarana]() 
 - [Dev parmar]()
 - [Shivangi Gajjar]()
 - [Viranya Shah]()
 - [Nupur Mehta]()
 - [Dreamy Pujara]()
 - [Rahul Vansh]()
 - [Meet Shah]()
 - [Krunal Ranpara]()
 - [Mrudang]() 

more details on individual contribution can be found [here](/Dataset/README.md)

## Authors

[Tarang Ranpara](https://in.linkedin.com/in/tarangranpara)

This project is developed and maintained at @ [IRLAB, DAIICT](http://irlab.daiict.ac.in/) under the guidence of [Prof. Prasenjit Majumder](https://in.linkedin.com/in/prasenjit-majumder-15a74720).  


## License Information

[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/tterb/atomic-design-ui/blob/master/LICENSEs)
