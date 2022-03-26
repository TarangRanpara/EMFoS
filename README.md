
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

we wanted a dataset containing news articles, human written summaries, news titles and human ratings for summaries. Since there was no such dataset available, we took a sample from one of such already available dataset, and generated abstractive summaries of news articles using a transformer based model, and had some people rate it on some qualitative measures. 

Therefore, one unique contribution of this project is a dataset containing human ratings for machine generated summaries. 

More information about the dataset can be found [here](https://github.com/TarangRanpara/EMFoS/blob/main/Dataset/README.md). 
        

### Computing correlation

Once the human ratings were collected, we needed to create a score that is representative of qualitative measures we took ratings for. we can take that score and compute its correlation with different metrics to know which metric is a better proxy for human evaluation.      

more about these metrics can be found [here](/Notebooks/README.md). 

## Results 

Detailed comparison of various evaluation metrics with human judgment with Significance testing can be found [here](https://docs.google.com/spreadsheets/d/1FdVI9LMi-UzOSfdZsdJBWsNYFlnYwAIJBZ5JVgewgvo/edit?usp=sharing). 

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

## Authors

[Tarang Ranpara](https://in.linkedin.com/in/tarangranpara)

This project is developed and maintained at @ [IRLAB, DAIICT](http://irlab.daiict.ac.in/) under the guidence of [Prof. Prasenjit Majumder](https://in.linkedin.com/in/prasenjit-majumder-15a74720).  

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


## License Information

[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/tterb/atomic-design-ui/blob/master/LICENSEs)
