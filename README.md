# nlp4if

`Attribute Classification` of COVID-19-Related Tweets Based on Natural Language Processing Models (`Student Research Training Program`)

## Introduction

Our work is based on [NLP4IF-Workshop--Shared-Task-On-Fighting the COVID-19 Infodemic](https://github.com/Veneziahhh/nlp4if/blob/main/nlp4if.md).

The major task is to predict a series of `binary attributes` of COVID-19 Twitter from seven aspects. The first, sixth and seventh questions are whether it is a `Verifiable Factual Claim`, whether it is `Harmful to Society` and whether it `Requires Attention`. The second, third, fourth and fifth questions are based on the first question. If it is a factual statement, then it is necessary to further judge whether it is `False Information`, whether it arouses `Interest to General Public`, what is the `Harmfulness` and `Need of Verification`. 

This is a multi task problem, and there is a dependency between tasks.

The dataset includes Twitter in `English`, `Bulgarian` and `Arabic`. 

- ###### Example of raw data

 <img src="https://user-images.githubusercontent.com/58615742/202167251-c7fe2c14-ad2c-4ab5-86ab-94a0aa8a2233.png" alt="image" style="zoom: 67%;" />

Because it is the real comment on Twitter, it inevitably contains `emoji` and `URL`, which brings some challenges to data preprocessing.

## Pipline

Inspired by the design and ideas in [Multi Output Learning using Task Wise Attention for Predicting Binary Properties of Tweets : Shared-Task-On-Fighting the COVID-19 Infodemic](https://aclanthology.org/2021.nlp4if-1.16.pdf) that ranked second in the competition at that time, we established our baseline and made further improvements to the training pipeline.

![image](https://user-images.githubusercontent.com/58615742/202171337-07520278-0f0b-40b9-83f7-f9eeba019891.png)

### Data Augmentation

Adopted by keeping labels on different language training datasets and mutual translation in the `data preprocessing stage`. 
<img src="https://user-images.githubusercontent.com/58615742/202177576-5255e6b5-2b37-456c-bfb2-00a80acd9a94.png" alt="image"  />

### Pre-training

`Bert`, `RoBERTa`, `XLM-RoBERTa` models are used in the `pre-training` stage.
![image](https://user-images.githubusercontent.com/58615742/202177768-3c13270f-bd42-4b20-b9d1-d49587e253fe.png)

### Classifier

`BiLSTM+Attn`, `TextCNN`, `MultiHead Attn` models are utilized in the `classifier`.

![image](https://user-images.githubusercontent.com/58615742/202178039-d5565820-be38-4216-b63a-9e2011ae5cec.png)

![image](https://user-images.githubusercontent.com/58615742/202178291-837c3a99-8626-4e54-8450-05fd53cd232a.png)

![image](https://user-images.githubusercontent.com/58615742/202179137-52c5c6ab-1afc-409b-bd24-5b44606fa601.png)

### Loss Function

`Loss function` with `biased weights` is improved on the basis of the `Uniform weights` in the [original paper](https://aclanthology.org/2021.nlp4if-1.16.pdf).
![image](https://user-images.githubusercontent.com/58615742/202179580-e72ece6b-499c-4c16-bac8-26cfcbd49589.png)

### Ensemble

Finally, we propose a voting mechanism. There are two schemes: `All vote` and `Top6 vote`.
![image](https://user-images.githubusercontent.com/58615742/202179899-25073f30-bb4f-4060-b02b-c6c0791c0b50.png)

## Results

After the attempt and optimization, taking Mean F1 Core as the standard, we trained 12 models, some of which far surpassed the best average F1-score of `89.7%` in [Fighting the COVID-19 Infodemic with a Holistic BERT Ensemble](https://aclanthology.org/2021.nlp4if-1.18.pdf), including Roberta-lstm-attn (`91.38%`), xlmRoberta-lstm-attn (`91.09%`), xlmRoberta-lstm-attn-biasedWeight (`90.67%`), xlmRoberta-multihead (`90.49%`), etc., optimized the training result by adopting voting mechanism and reached an ultimate best-vote of `93.54%`.
