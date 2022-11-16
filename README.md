# nlp4if

`Attribute Classification` of COVID-19-Related Tweets Based on Natural Language Processing Models (`Student Research Training Program`)



Our work is based on [NLP4IF-Workshop--Shared-Task-On-Fighting the COVID-19 Infodemic](https://github.com/Veneziahhh/nlp4if/blob/main/nlp4if.md).

The major task is to predict a series of `binary attributes` of COVID-19 Twitter from seven aspects. The first, sixth and seventh questions are whether it is a `Verifiable Factual Claim`, whether it is `Harmful to Society` and whether it `Requires Attention`. The second, third, fourth and fifth questions are based on the first question. If it is a factual statement, then it is necessary to further judge whether it is `False Information`, whether it arouses `Interest to General Public`, what is the `Harmfulness` and `Need of Verification`. 

This is a multi task problem, and there is a dependency between tasks.

The dataset includes Twitter in `English`, `Bulgarian` and `Arabic`. 

###### Example of raw data:

 <img src="https://user-images.githubusercontent.com/58615742/202167251-c7fe2c14-ad2c-4ab5-86ab-94a0aa8a2233.png" alt="image" style="zoom: 67%;" />


Because it is the real comment on Twitter, it inevitably contains `emoji` and `URL`, which brings some challenges to data preprocessing.

Inspired by the design and ideas in [Multi Output Learning using Task Wise Attention for Predicting Binary Properties of Tweets : Shared-Task-On-Fighting the COVID-19 Infodemic](https://aclanthology.org/2021.nlp4if-1.16.pdf) that ranked second in the competition at that time, we established our baseline and made further improvements to the training pipeline.

![image](https://user-images.githubusercontent.com/58615742/202171337-07520278-0f0b-40b9-83f7-f9eeba019891.png)

`Data Augmentation` is adopted by keeping labels on different language training datasets and mutual translation in the `data preprocessing stage`. `Bert`, `RoBERTa`, `XLM-RoBERTa` models are used in the `pre-training` stage, `bidirectional LSTM attn`, `TextCNN`, `MultiHead Attn` models are utilized in the `classifier`, and the `Loss function` is improved on the basis of the `Uniform weights` in the [original paper](https://aclanthology.org/2021.nlp4if-1.16.pdf). Finally, we propose a voting mechanism. There are two schemes: `All vote` and `Top6 vote`.

After the attempt and optimization, taking Mean F1 Core as the standard, we trained 12 models, some of which far surpassed the best average F1-score of `89.7%` in [Fighting the COVID-19 Infodemic with a Holistic BERT Ensemble](https://aclanthology.org/2021.nlp4if-1.18.pdf), including Roberta-lstm-attn (`91.38%`), xlmRoberta-lstm-attn (`91.09%`), xlmRoberta-lstm-attn-biasedWeight (`90.67%`), xlmRoberta-multihead (`90.49%`), etc., optimized the training result by adopting voting mechanism and reached an ultimate best-vote of `93.54%`.
