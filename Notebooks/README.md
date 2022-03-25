## Notebooks 

This directory contains code for computing scores of supported evaluation metrics and their correlation with human ratings. 

## Directory Structure

```
EMFoS 
│
└───Notebooks 
│   │   ComputePearsonCorrelation.ipynb
|   |   ComputeSpearmanCorrelation.ipynb
|   |   ComputeScores.ipynb
|   |   README.md
|   
```   

## List of Evaluation Metrics considered 

Below is the list of the evaluation metrics we took into consideration. 

|Evaluation Metrics| Description|
| :---        | :--- |
|**R1**|	ROUGE1 |
|**R2**|	ROUGE2|
|**RL**|	ROUGEL|
|**CS1**|	sentence-transformers/sentence-t5-xl|
|**CS2**|	sentence-transformers/sentence-t5-large |
|**CS3**|	sentence-transformers/multi-qa-MiniLM-L6-cos-v1|
|**CS4**|	sentence-transformers/distiluse-base-multiling... |
|**CS5**|	sentence-transformers/paraphrase-MiniLM-L6-v2|
|**CS6**|	bert-base-uncased|
|**CS7**|	roberta-base, roberta|
|**CS8**|	en_core_web_sm|
|**CS9**|	en_core_web_md|
|**CS10**|	en_core_web_lg|
|**CS11**|	word2vec-google-news-300|
|**CS12**|	glove-twitter-25|
|**BS00**|	bert-base-uncased|
|**BS01**|	bert-large-uncased|
|**BS02**|	bert-base-cased-finetuned-mrpc|
|**BS03**|	roberta-base|
|**BS04**|	roberta-large|
|**BS05**|	roberta-large-mnli|
|**BS06**|	facebook/bart-base|
|**BS07**|	facebook/bart-large|
|**BS08**|	facebook/bart-large-cnn|
|**BS09**|	facebook/bart-large-mnli|
|**BS10**|	facebook/bart-large-xsum|
|**BS11**|	t5-small|
|**BS12**|	t5-base|
|**BS13**|	t5-large|
|**BS14**|	microsoft/deberta-base|
|**BS15**|	microsoft/deberta-base-mnli|
|**BS16**|	microsoft/deberta-large|
|**BS17**|	microsoft/deberta-large-mnli|
|**BS18**|	microsoft/deberta-xlarge|
|**BS19**|	microsoft/deberta-xlarge-mnli|
|**BS20**|	google/pegasus-xsum


## Correlation Methology 

1. Compute scores for given summary using supported evaluation metrics. 
2. Take data from both sets and average out the ratings 
3. Normalize between [0-1]
4. From normalized average scores, make two variants of human evaluation score. (one variant is weighted average of qualitative params and another is subjective score) 
5. Measure pearson and spearman-rank correlation of both variant with each scores computed in step-1.    

