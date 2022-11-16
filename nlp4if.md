# NLP4IF-Workshop--Shared-Task-On-Fighting the COVID-19 Infodemic

The task is about predicting several binary properties of a tweet about COVID-19: whether it is harmful, whether it contains a verifiable claim, whether it may be of interest to the general public, whether it appears to contain false information, etc..

This repository contains the _dataset_, _format checker, scorer and baselines_ for the NLP4IF Workshop shared task.

**Leaderboard**: </br>
All results can be found here, https://tinyurl.com/2drvrucv. </br>
**NOTE:** The scores have been updated on Apr 10, 2021 (14:00 PM GMT/UTC time)

**Submission**: </br>
Submit your predictions using the following form: https://tinyurl.com/yh25a99x.

**Important Dates:**
- February 24, 2021: Training data released
- April 6, 2021: Test input released
- April 8, 2021: Test submissions due
- April 12, 2021: System descriptions due
- April 19, 2021: System descriptions notification of acceptance
- April 26, 2021: Camera-ready system descriptions due (hard deadline)


__Table of contents:__

- [Fighting the COVID-19 Infodemic](#CLARIN-Hackathon-2020-Fighting-the-COVID19-Infodemic)
  - [System Description Submissions](#System-Description-Submissions)
  - [Evaluation Results](#evaluation-results)
  - [List of Versions](#list-of-versions)
  - [Data Annotation](#data-annotation)
  - [Data Format](#data-format)
    - [Input Dataset](#input-dataset)
    - [Results File](#results-file)
  - [Format checkers](#format-checkers)
  - [Scorers](#scorers)
    - [Evaluation metrics](#evaluation-metrics)
  - [Licensing](#licensing)
  - [Credits](#credits)
  - [Citation](#citation)

## System Description Submissions

If you want to submit a system description paper, please submit your paper through the softconf system, https://www.softconf.com/naacl2021/nlp4if2021/.

The paper should be up to 4 pages long with unlimited references. See the guidelines here: https://2021.naacl.org/calls/style-and-formatting/


## Evaluation Results

All results can be found here, https://tinyurl.com/2drvrucv. 

## List of Versions
* __test-input [2021/04/06]__ - Test input data for English subtasks
* __test-input [2021/04/06]__ - Test input data for Arabic subtasks
* __test-input [2021/04/06]__ - Test input data for Bulgarian subtasks
* __v3.0 [2021/04/04]__ - Additional training/dev data for English subtasks
* __v3.0 [2021/04/04]__ - Additional training data for Arabic subtasks
* __v1.0 [2021/02/23]__ - Training/Dev data for English subtasks
* __v1.0 [2021/02/23]__ - Training/Dev data for Arabic subtasks
* __v1.0 [2021/02/23]__ - Training/Dev data for Bulgarian subtasks

## Data Annotation

The annotation of the tweets were done according to the following guidelines found in this [link](https://micromappers.qcri.org/project/covid19-tweet-labelling/tutorial).

The 7 quesitons asked were, 

1. *Verifiable Factual Claim: Does the tweet contain a verifiable factual claim?*
A verifiable factual claim is a sentence claiming that something is true, and this can be verified using factual, verifiable information such as statistics, specific examples, or personal testimony.

Factual claims include the following:
- Stating a definition;
- Mentioning quantity in the present or the past;
- Making a verifiable prediction about the future;
- Reference to laws, procedures, and rules of operation;
- References to images or videos (e.g., "This is a video showing a hospital in Spain.'');
- Statements about correlations or causations. Such correlation and causation needs to be explicit, i.e., sentences like "This is why the beaches haven't closed in Florida. (https://t.co/8x2tcQeg21)[https://t.co/8x2tcQeg21]'' is not a claim because it does not say why explicitly, thus it is not verifiable.

2. *False Information: To what extent does the tweet appear to contain false information?*
The stated claim may contain false information. This question labels the tweets with the categories mentioned below. False Information appears on social media platforms, blogs, and news-articles to deliberately misinform or deceive the readers.

3. *Interest to General Public: Will the tweet have an effect on or be of interest to the general public?*
Most often people do not make interesting claims, which can be verified by our general knowledge. For example, "Sky is blue'' is a claim, however, it is not interesting to the general public. In general, topics such as healthcare, political news and findings, and current events are of higher interest to the general public. Using the five point Likert scale the labels are defined below.

4. *Harmfulness: To what extent is the tweet harmful to the society/person(s)/company(s)/product(s)?*
The purpose of this question is to determine if the content of the tweet aims to and can negatively affect the society as a whole, specific person(s), company(s), product(s) or spread rumors about them. The content intends to harm or weaponize the information. A rumor involves a form of a statement whose veracity is not quickly or ever confirmed.


5. *Need of Verification: Do you think that a professional fact-checker should verify the claim in the tweet?*
It is important to verify a factual claim by a professional fact-checker, which can cause harm to the society, specific person(s), company(s), product(s) or government entities. However, not all factual claims are important or worthwhile to be fact-checked by a professional fact-checker as it is a time-consuming procedure. Therefore, the purpose is to categorize the tweet using the labels defined below. While doing so annotator can rely on the answers to the previous questions. 


6. *Harmful to Society: Is the tweet harmful for the society and why?*
The purpose of this question is to categorize if the content of the tweet is intended to harm the society or weaponized to mislead the society. To identify that we defined the following labels for the categorization:
  - NO, not harmful
  - NO, joke or sarcasm
  - YES, panic
  - YES, xenophobic, racist, prejudices or hate-speech
  - YES, bad cure
  - YES, rumor or conspiracy
  - YES, other

7. *Require attention: Do you think that this tweet should get the attention of government entities?*
Most often people tweet by blaming authorities, providing advice, and/or calls for action. Sometime that information might be useful for any government entity to make a plan, respond or react on it. The purpose of this question is to categorize such information. It is important to note that not all information requires attention for a government entity. Therefore, even if the tweet shows information belong to any of the positive categories, however, it is important to understand whether that requires government attention. For the annotation, it is mandatory to first decide on whether attention is necessary for 
government entities

## Data Format

### Input Dataset

The datasets are TAB separated text files. The text encoding is UTF-8. 
A row of the file has the following format:

> tweet_no <TAB> tweet_text <TAB> q1_label <TAB> q2_label <TAB> q3_label <TAB> q4_label <TAB> q5_label <TAB> q6_label <TAB> q7_label

Where: <br>
* tweet_no: index of the tweet (used to get tweet ID from the _id.tsv) <br/>
* tweet_text: content of the tweet <br/>
* q__n_label: label yes/no or nan for quesiton__n <br/>

Example:
> 1	For the average American the best way to tell if you have covid-19 is to cough in a rich person’s face and wait for their test results	no	nan	nan	nan	nan	no	no <br/>
> 2	this is fucking bullshit	no	nan	nan	nan	nan	no	no <br/>
> ... <br/>


### Results File

For this task, the expected results file is a list of tweets with the predicted label for each of the 7 questions. 

> Q1_p <TAB> Q2_p <TAB> Q3_p <TAB> Q4_p <TAB> Q5_p <TAB> Q6_p <TAB> Q7_p <TAB>

Where: <br>
* Q1_p: should be either yes/no depending on the answer to the first question as described in [Data Annotation](#data-annotation). <br/>
* Q2_p: should be either yes/no depending on the answer to the second question as described in [Data Annotation](#data-annotation) or nan if Q1_p is no. <br/>
* Q3_p: should be either yes/no depending on the answer to the third question as described in [Data Annotation](#data-annotation) or nan if Q1_p is no. <br/>
* Q4_p: should be either yes/no depending on the answer to the fourth question as described in [Data Annotation](#data-annotation) or nan if Q1_p is no. <br/>
* Q5_p: should be either yes/no depending on the answer to the fifth question as described in [Data Annotation](#data-annotation) or nan if Q1_p is no. <br/>
* Q6_p: should be either yes/no depending on the answer to the sixth question as described in [Data Annotation](#data-annotation). <br/>
* Q7_p: should be either yes/no depending on the answer to the seventh question as described in [Data Annotation](#data-annotation). <br/>

Example:
> yes	no	yes	no	yes	no	no<br/>
> yes	no	yes	no	yes	no	no<br/>
> no	nan	nan	nan	nan	yes	no<br/>
> ... <br/>

## Format checkers

The checker for the subtask is located in the [format_checker](format_checker) module of the project.
The format checker verifies that your generated results file complies with the expected format.
To launch it run: 
> python3 format_checker/main.py --pred_file_path=<path_to_your_results_file> <br/>

Note that the checker can not verify whether the prediction file you submit contain all lines/tweets, because it does not have access to the corresponding gold file.

## Scorers

Launch the scorer for the task as follows:
> python3 scorer/main.py --gold_file_path="path_gold_file" --pred_file_path="predictions_file" <br/>

__<path_to_gold_file>__ is the path to the file containing the gold annotations and __<predictions_file>__ is the path to the corresponding file with participants' predictions, which must follow the format, described in the 'Results File Format' section.

The scorer invokes the format checker for the task to verify the output is properly shaped.
It also handles checking if the provided predictions file contains all lines / tweets from the gold one.

### Evaluation metrics

The official evaluation measure is F1, but we also report (Accuracy, Recall and Precision). 

## Licensing

  These datasets are free for general research use.

## Credits

Organizers:
- Shaden Shaar, Qatar Computing Research Institute, HBKU
- Firoj Alam, Qatar Computing Research Institute, HBKU
- Giovanni Da San Martino, University of Padova
- Alex Nikolov, Sofia University
- Wajdi Zaghouani, Hamad bin Khalifa University
- Preslav Nakov, Qatar Computing Research Institute, HBKU


## Citation

```
@inproceedings{NLP4IF-2021-COVID19-task,
    title = "Findings of the {NLP4IF}-2021 Shared Task on Fighting the {COVID}-19 Infodemic and Censorship Detection",
    author = "Shaar, Shaden and
      Firoj Alam and
      Da San Martino, Giovanni and
      Nikolov, Alex and
      Zaghouani, Wajdi and
      Nakov, Preslav and
      Feldman, Anna",
    booktitle = "Proceedings of the Fourth Workshop on Natural Language Processing for Internet Freedom: Censorship, Disinformation, and Propaganda",
    series = {NLP4IF@NAACL'~21},
    month = {June},
    year = "2021",
    address = "Online",
    publisher = "Association for Computational Linguistics",
}
```

