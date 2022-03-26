## Dataset

We decided to take the [Indian News Dataset](https://www.kaggle.com/datasets/sunnysai12345/news-summary), a collection of news articles, news titles, and their respective human-written summaries (scraped from [Inshorts](https://www.inshorts.com/)).

We did some pre-processing on the dataset mentioned above, took a sample of 1001 tuples, and generated abstractive summaries using [bart-large-cnn](https://huggingface.co/facebook/bart-large-cnn). we used in-house [django-based tool](https://github.com/TarangRanpara/SummaryAnnotatorTool) for collecting human ratings. 

We asked our reviewers to rate the given summary between [1-5] on the following Qualitative measures. 

-  Grammatical Correctness
-  Arrangement of sentences/Flow of information
-  Text Quality
-  Conciseness
-  Exhaustiveness
-  Overall Rating (subjective to the annotator)

Since the ratings can be subjective to a reviewers' understanding, we got two distinct sets of people to rate these same 1001 samples. 

## Dataset Structure

As mentioned in the [main README](/README.md) file, we collected two sets of annotations for the same set of summaries. Therefore, for each summary, we have 2 sets of results for Qualitative Measures like Grammatical Correctness, Arrangement/Flow of information, Text Quality, Conciseness, Exhaustiveness, and SubjectiveScore. 

The dataset contains 1001 rows and below mentioned columns. 

| Column      | Type | Description |
| :---        | :--- | :--- |           
| summaryID      | INT | Unique ID       |
| candidate   | STRING | Machine Generated (Candidate) summary        |
| gold| STRING | Human written (reference) summary |
| title| STRING | News Title |
| grammatical_correctness_1| INT | 1-5 Rating for Grammatical Correctness in **Set-1** |
| arrangement_1| INT | 1-5 Rating for Arrangement/Flow of information in **Set-1** |
| quality_1| INT | 1-5 Rating for Text Quality in **Set-1** |
| conciseness_1| INT | 1-5 Rating for Conciseness in in **Set-1**|
| exhaustiveness_1| INT | 1-5 Rating for Exhaustiveness in **Set-1**|
| subjectiveScore_1| INT | 1-5 Rating given to the summary as a whole in **Set-1** |
| annotator_1| STRING | Name of Annotator in **Set-1**|
| grammatical_correctness_2| INT | 1-5 Rating for Grammatical Correctness in **Set-2** |
| arrangement_2| INT | 1-5 Rating for Arrangement/Flow of information in **Set-2** |
| quality_2| INT | 1-5 Rating for Text Quality in **Set-2**|
| conciseness_2| INT | 1-5 Rating for Conciseness in **Set-2**|
| exhaustiveness_2| INT | 1-5 Rating for Exhaustiveness in **Set-2** |
|subjectiveScore_2| INT | 1-5 Rating given to the summary as a whole in **Set-2**|
| annotator_2| STRING | Name of Annotator in **Set-2**|
| url| STRING | URL of original article |

## Instructions given to reviewer for rating each of the above columns

- **Grammatical Correctness**
      
      - check if the generated summary is grammatically correct. (check common mistakes)
      - check spelling mistakes, sentence formations, use of punctuations, etc.
      - Ignore "?" (question mark) if it appears at incorrect positions. It probably represents styled single or double quotes that Django doesn't support.   

- **Arrangement of sentences/flow of information**

      - Read the title, and reference summary to rate the flow of information.
      - Observe the flow of information and check if it makes sense.

- **Text Quality**

      - How pleasant is it to read?
      - Ex. check that sentences aren't too long
      - Does the writing style suit the intended audience? In this case, our audience is newsreaders.
      - News is supposed to be direct, should sound professional, and should not use slang words unless it's quoting something.

- **Conciseness**

      - Read the title, and reference summary to rate the Conciseness.
      - check if the summary is concise and it addresses the single most important point. some summaries tend to get into giving brief background info at first but that is fine.
      - It should not stumble between multiple sub topics.

- **Exhaustiveness**

      - Read the title, and reference summary to rate the Exhaustiveness.
      - Check if the summary contains enough details.
      - A summary should contain enough details about the topic it's focusing on.
      - Ex. If the summary is about some comapny's share going up, the summary should contain details about why it went up, margin by which it went up, etc.

- **Overall Rating**
      
      - Read the title, and reference summary to rate the Machine Generated Summary overall.

## Contributors 

Total 30 people took part in the dataset building process, out of which nine contributed in Set-1 (also called "Inside"), and 21 contributed in Set-2(also called "Outside").


Contribution distribution of Set-1: 

![set-1](/Assets/Inside%20DAIICT%20(Set-1).png)


Contribution distribution of Set-2: 

![set-2](/Assets/outside%20DAIICT%20(Set-2).png)

Qualification distribution of Annotators (overall): 

![Qualification](/Assets/Distribution%20of%20Qualification.png)




