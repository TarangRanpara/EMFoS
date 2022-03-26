## Notebooks 

For building a score out of human judgments, we first averaged the scores from both annotations to counter the subjectivity of opinions.

From the collected human judgments, we computed two kinds of scores. 

- **Score-1:** Used "Overall Rating" Score directly (also called "OVERALL SCORE")
- **Score-2:** took a Weighted average of qualitative measures (except "Overall Rating") listed above (also called "WEIGHTED SCORE").

We then computed the correlation of score-1 and score-2 with a set of candidate evaluation metrics falling broadly into three categories. 
- N-Gram Overlap
- Contextual Similarity
- Pairwise Contextual Similarity

### N-Gram Overlap
    
[ROUGE Score](https://aclanthology.org/W04-1013/) measures n-gram overlap between candidate and gold standard summary. 

we have considered ROUGE-1, ROUGE-2 and ROUGE-L.  

### Contextual Similarity

We computed cosine similarity of document embeddings of candidate and gold standard for measuring contextual similarity. 


For computing document embeddings, we used **four** different varieties of methods. 

| Type of model      | Description |
| :---        | :--- |
| Gensim based models |Computes the average of word embeddings to get document embeddings.|
| Spacy Models | Directly used in-built functionality to get the document embeddings. |
| Vanilla Transformers (with Bert-like architecture) | Computed embeddings of [CLS] token. [CLS] token is prepended at the start of any sentence(s) by the transformer tokenizer.  |
| Sentence-transformers | Directly used in-built functionality to get the document embeddings.|

### Pairwise Contextual Similarity
    
we experimented by using different models in [BertScore](https://github.com/Tiiiger/bert_score). 

![BertScore](/Assets/bert_score.png)

## List of Evaluation metrics considered 

Below is the list of the evaluation metrics we took into consideration. 

|Evaluation Metrics| Description| Type |
| :---        | :--- | :--- |
|**R1**|	ROUGE1 | N-Gram Overlap |
|**R2**|	ROUGE2| N-Gram Overlap |
|**RL**|	ROUGEL| N-Gram Overlap |
|**CS1**|	sentence-transformers/sentence-t5-xl| Contextual Similarity |
|**CS2**|	sentence-transformers/sentence-t5-large | Contextual Similarity |
|**CS3**|	sentence-transformers/multi-qa-MiniLM-L6-cos-v1| Contextual Similarity |
|**CS4**|	sentence-transformers/distiluse-base-multiling... | Contextual Similarity |
|**CS5**|	sentence-transformers/paraphrase-MiniLM-L6-v2| Contextual Similarity |
|**CS6**|	bert-base-uncased| Contextual Similarity |
|**CS7**|	roberta-base, roberta| Contextual Similarity |
|**CS8**|	en_core_web_sm| Contextual Similarity |
|**CS9**|	en_core_web_md| Contextual Similarity |
|**CS10**|	en_core_web_lg| Contextual Similarity |
|**CS11**|	word2vec-google-news-300| Contextual Similarity |
|**CS12**|	glove-twitter-25| Contextual Similarity |
|**BS00**|	bert-base-uncased| Pairwise Contextual Similarity |
|**BS01**|	bert-large-uncased| Pairwise Contextual Similarity |
|**BS02**|	bert-base-cased-finetuned-mrpc| Pairwise Contextual Similarity |
|**BS03**|	roberta-base| Pairwise Contextual Similarity |
|**BS04**|	roberta-large| Pairwise Contextual Similarity |
|**BS05**|	roberta-large-mnli| Pairwise Contextual Similarity |
|**BS06**|	facebook/bart-base| Pairwise Contextual Similarity |
|**BS07**|	facebook/bart-large| Pairwise Contextual Similarity |
|**BS08**|	facebook/bart-large-cnn| Pairwise Contextual Similarity |
|**BS09**|	facebook/bart-large-mnli| Pairwise Contextual Similarity |
|**BS10**|	facebook/bart-large-xsum| Pairwise Contextual Similarity |
|**BS11**|	t5-small| Pairwise Contextual Similarity |
|**BS12**|	t5-base| Pairwise Contextual Similarity |
|**BS13**|	t5-large| Pairwise Contextual Similarity |
|**BS14**|	microsoft/deberta-base| Pairwise Contextual Similarity |
|**BS15**|	microsoft/deberta-base-mnli| Pairwise Contextual Similarity |
|**BS16**|	microsoft/deberta-large| Pairwise Contextual Similarity|
|**BS17**|	microsoft/deberta-large-mnli| Pairwise Contextual Similarity|
|**BS18**|	microsoft/deberta-xlarge| Pairwise Contextual Similarity|
|**BS19**|	microsoft/deberta-xlarge-mnli| Pairwise Contextual Similarity|
|**BS20**|	google/pegasus-xsum | Pairwise Contextual Similarity |


## Correlation Methology 

1. Compute scores for given summary using supported evaluation metrics. 
2. Take data from both sets and average out the ratings 
3. Normalize between [0-1]
4. From normalized average scores, make two variants of the human evaluation score. (one variant is a weighted average of qualitative params and another is a subjective score) 
5. Measure Pearson and spearman-rank correlation of both variants with each score computed in step-1.    

## Directory Structure

- **ComputeScores.ipynb** : Compute the results using evaluation metrics mentioned above.  
- **ComputePearsonCorrelation.ipynb**: compute Pearson Correlation between evaluation metrics and score-1 and score-2.
- **ComputeSpearmanCorrelation.ipynb** : compute Spearman Correlation between evaluation metrics and score-1 and score-2.

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

