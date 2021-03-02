---
title: "Evaluation Metrics for Binary Classification in Machine Learning: When Accuracy Score Is Not Enough"
date: 2021-3-2
tags: [machine learning, binary classification]
header:
excerpt: "machine learning, binary classification"
---

# Evaluation Metrics for Binary Classification in Machine Learning: When Accuracy Score Is Not Enough

At work and in our everyday life, we often make decisions that have two potential outcomes (true or false, acceptance or rejection, etc.). A type of machine learning algorithms, namely binary classification, can automate this process. However, we need to always bear in mind what our ultimate goals are and make sure that algorithms are set up to achieve these goals.  

## Evaluation metrics, accuracy score and its shortcomings

Roughly speaking, evaluation metrics are used to judge how well a machine learning model achieves a pre-specified goal. Consider a scenario where a bank tries to predict whether a person defaults on credit card loans using demographic and professional data. You are provided with two algorithms A and B, and check their predictions against the actual outcomes, You get the following tables:
  
  - Algorithm 1

|                         | Predicted: default | Predicted: non-default | Sum |
  |------------------------:|--------------------|------------------------|-----|
  | Actual: default         | 5                  | 5                      | 10  |
  | Actual: non-default     | 10                 | 80                     | 90  |
  | Sum                     | 15                 | 85                     | 100 |
  
  Among the 10 actual default cases, Algorithm 1 predicted that 5 of them would default and 5 of them would not. Among then 90 actual non-default cases, the algorithm predicted that 10 of them would default and 80 of them would not. 

- Algorithm 2

|                         | Predicted: default | Predicted: non-default | Sum |
  |------------------------:|--------------------|------------------------|-----|
  | Actual: default         | 1                  | 9                      | 10  |
  | Actual: non-default     | 2                  | 88                     | 90  |
  | Sum                     | 3                  | 97                     | 100 |
  
  Among the 10 actualy default cases, Algorithm 2 predicted that 1 of them would default and 9 of them would not. Among then 90 actual non-default cases, the algorithm predicted that 2 of them would default and 88 of them would not. 

Which algorithm is better? It depends on the evaluation metric. A common one for binary classification is accuracy score, which is defined as the following:
  
  $$accuracy\ score = \frac{total\ number\ of\ correct\ predictions}{total\ number\ of\ predictions}$$
  
  When a actual default case is predicted as default, or an actual non-default case is predicted as non-defult, a prediction is correct. Otherwise, a prediction is incorrect. 

The accuracy score for Algorithm 1 is calculated below:
  
  $$accuracy\ score\  1= \frac{5 + 80}{100} = 0.85$$
  
  The accuracy score for Algorithm 2 is calculated below:
  
  $$accuracy\ score\  1= \frac{1 + 88}{100} = 0.89$$
  
  Does this mean that Algorithm 2 is better than Algorithm 1? A financial analyst would disagree. In fact, Algorithm 2 is of little value at all since it only successfully distinguishes one default case from non-default cases. By contrast, Algorithm 1 is able to successfully identify 5 out of 10 actual default cases. **For a bank, it is more important to identify those who will default that to identify those who will not defaul**, because most people do not default and those who do can cause big damage to a bank's profitability. Therefore, accuracy score is not an appropriate evaluation metric here. 

## Alternatives to accuracy score: precision and recall

There are many other alternative evaluation metrics to accuracy score. Precision and recall are most widely used. 

### Positive and negative classes

Before using these two metrics, we need to dig back into the real-world question and decide which of the two potential outcomes (default and non-default) we care more about. In the above example, from a profit-making point of view, the bank would care more about default clients than non-default ones. As a result, in machine learning jargons, we call the default class positive, and the non-default class negative. 

### Precision

Precision measures among all instances that are predicted as positive, how many of them are actually positive. For Algorithm 1, the precision is:

$$precision\ 1= \frac{5}{15} = 0.33$$

For Algorithm 2, it is:

$$precision\ 2= \frac{1}{3} = 0.33$$

### Recall

Recall measures among all instances that are acutally positive, how many of them are successfully identified as positive. For Algorithm 1, the recall is:

$$recall\ 1= \frac{5}{10} = 0.5$$

For Algorithm 2, it is:

$$precision\ 2= \frac{1}{9} = 0.1$$

Although Algorithms 1 and 2 have the same precision, the recall of Algorithm 1 is much higher. Therefore, we think Algorithm 1 is better than Algorithm 2. 

## Back to the real world: modeling outcome and broader applications

Does our choice make sense? Let us test it against a real world scenario. 

- Financial returns for bank

|                         | Predicted: default | Predicted: non-default |
|------------------------:|--------------------|------------------------|
| Actual: default         | 0                  | -50                    |
| Actual: non-default     | 0                  | 5                      |

As shown in the table above, if a bank predicts that a customer would default, it will choose not to extent loan, and thus the financial return is zero regardless whether the customer defaults or not. If the bank issues a loan and the customer does not default, the bank will earn 5 dollars' profit in average. However, if a customer is issued a loan and defaults, the bank will suffer from 50 dollars' loss. 

The net profit for the bank, using Algorithm 1, is:

$$0 \times 5 + 0 \times 10 + (-50) \times 5 + 5 \times 80 = 150$$

Using Algorithm 2, the bank's net profit is:
  
  $$0 \times 1 + 0 \times 2 + (-100) \times 9 + 5 \times 88 = -460$$
  
  Algorithm 1 indeed gives the bank a better financial outcome! The use of evaluation metrics other than accuracy score is applied to many real-world questions. For example, if we want to detect a rare disease from blood samples of the general population, we should set the "have disease" outcome as the positive class, and select an algorithm that detects enough real patients, even if a reasonable amount of non-patients are erroreously also categorized as having the disease. We can always do follow-up the checks to make sure that we do not give treatment to people who do not have the disease. 