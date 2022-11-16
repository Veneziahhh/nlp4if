# nlp4if

`Attribute Classification` of COVID-19-Related Tweets Based on Natural Language Processing Models (`Student Research Training Program`)



Our work is based on [NLP4IF-Workshop--Shared-Task-On-Fighting the COVID-19 Infodemic](https://github.com/Veneziahhh/nlp4if/blob/main/nlp4if.md).

The major task is to predict a series of `binary attributes` of COVID-19 Twitter from seven aspects. The first, sixth and seventh questions are whether it is a `Verifiable Factual Claim`, whether it is `Harmful to Society` and whether it `Requires Attention`. The second, third, fourth and fifth questions are based on the first question. If it is a factual statement, then it is necessary to further judge whether it is `False Information`, whether it arouses `Interest to General Public`, what is the `Harmfulness` and `Need of Verification`. 

This is a multi task problem, and there is a dependency between tasks.

The dataset includes Twitter in `English`, `Bulgarian` and `Arabic`. 

###### Example of raw data:

 ![image](https://user-images.githubusercontent.com/58615742/202167251-c7fe2c14-ad2c-4ab5-86ab-94a0aa8a2233.png)


Because it is the real comment on Twitter, it inevitably contains emoji and URL, which brings some challenges to data preprocessing.



² Created a neural network for the training of the automated identifying of a COVID-19 tweet’s binary attribute

² Enhanced the data by keeping labels on different language training datasets and mutual translation in the data preprocessing stage 

² Used Bert, Roberta and XLM-Roberta to build pre-training models

² Utilized both LSTM+Attention and MultiHead Attention mechanisms, the CNN model and the adjustable Loss function in creating the classification models

² Trained 12 models that far surpass the best average F1-score of 89.7%, including Roberta-lstm-attn (91.38%), xlmRoberta-lstm-attn (91.09%), xlmRoberta-lstm-attn-biasedWeight (90.67%), xlmRoberta-multihead (90.49%), etc., optimized the training result by adopting voting mechanism and reached an ultimate best-vote of 93.54%

![image](https://user-images.githubusercontent.com/58615742/202171171-34b86831-3dd8-4ee6-a4da-e87c3f1f09a5.png)


