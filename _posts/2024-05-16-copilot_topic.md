---
title: "GitHub Copilot not working for your analytics project? Check sensitive keywords!"
date: 2024-5-16
tags: [artificial intelligence, large language models, safety and security]
header:
excerpt: "artificial intelligence, large language models, safety and security"
---

Generative Artificial Intelligence (genAI) has become an indispensable part of software and analytics development. As an R developer working with data analytics, visualization and computation optimization, 
I use tools like GitHub Copilot every day to improve my productivity and automate routine tasks. Recently, I have witnessed cases where Copilot seems to stop working, and after investigation, the reason, I believe, is 
the underlying genAI's safety measures that restrict certain kinds of outputs. 

It requires the utmost care to use the most power tools responsibly, and developers and analysts who use genAI tools should be aware of such safety measures and understand its implications. More importantly, on the top of safety measures included in the genAI, we should stay vigilant and take time to reflect: will my use of genAI create danger, harm or bias? 

## Why has my Copilot stopped working?

As an example, I create a few helper functions to analyze demographic data of some Canadian cities in R. GitHub Copilot is extremely powerful for such tasks: 

```{R}
library(tibble)

demo_data <- tibble(

  city = c("Toronto", "Montreal", "Vancouver", "Calgary", "Ottawa"),

  population = c(2731571, 1704694, 631486, 1237656, 934243),

  median_age = c(37.1, 39.3, 40.8, 36.6, 39.4),

  median_income = c(34500, 32000, 30000, 35000, 33000),

  immigrant_percent = c(46.1, 31.4, 40.8, 30.2, 23.6),

  university_percent = c(30.3, 25.4, 35.6, 28.7, 27.8),

  transgender_percent = c(0.5, 0.3, 0.4, 0.2, 0.1),

  data_scientist_percent = c(0.1, 0.2, 0.3, 0.4, 0.5)

)
```

I want to create functions that extract one aspect of information, for example, percentage of university-educated individuals, for selected cities. For example, I want to create a `get_population` function that does the following:

```{R}

get_population("Toronto")

# A tibble: 1 × 2
  city    population
  <chr>        <dbl>
1 Toronto    2731571

```

With very limited prompt, CoPilot is doing a great job creating functions for population, age and income:

<iframe width="560" height="315" src="https://www.youtube.com/embed/4Y2ti_G-73E" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The three functions created are all correct: 

`get_population`

`get_median_age`

`get_median_income`

Copilot is really smart, right? In my experience, this is the least Copilot can do for you in programming. 

Now we move on to the percentage of immigrants. As you can see below, Copilot suddenly seems reluctant to suggest anything:

<iframe width="560" height="315" src="https://www.youtube.com/embed/8xW1G19aX_o" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Specifically, Copilot is "stuck" at three places. One is after "should return the percentage of", following which should be the word "immigrants". Instead, I had to type it out myself. Two is after the first part of the function name "get_", following which should be "immigrant_percent". Again, I had to type it out myself. Three is after the `select` function, which should be `(city, immigrant_percent)`. 

**What is going on here?** Has Copilot suddenly become less smart? Let us continue with creating the rest of functions. 

**Woohoo!** Copilot is smart again! As you can see, 

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