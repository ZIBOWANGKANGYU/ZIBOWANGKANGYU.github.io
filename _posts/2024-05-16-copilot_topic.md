---
title: "GitHub Copilot seem hesitant? Could be AI safety and fairness measures!"
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

<span style="font-size:0.5em;">
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
</span>

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

**Woohoo!** Copilot is smart again! As you can see, Copilot had no problem creating the fifth function, `get_university_percent`, correctly.

<iframe width="560" height="315" src="https://www.youtube.com/embed/xpWXbAeKSYw" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

What about the percentage of transgender individuals? **Again, Copilot seems stuck**. GitHub seems reluctant to proceed at three places: 

<iframe width="560" height="315" src="https://www.youtube.com/embed/t4-MH_2Mbk0" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- At function description, after "should return the percentage of". We need the phrase "transgender individuals". 

- Name of the function, which should be "get_transgender_percent"

- In the `select` function, which should be `(city, transgender_percent)`

We are beginning to see that **keywords** ("immigrant" and "transgender") are playing an important role here. An alternative hypothesis is that while population, age, income and education are commonly analyzed demographic characteristics, immigration status and gender identity are less commonly studied. If this is indeed the case, Copilot should also have difficulty creating a function analyzing the percentage of data scientists. Whether somebody works in data science is not a question asked in Canadian censuses, but immigration status is. 

It turns out this is not the case. Copilot had zero problem creating `get_data_scientist_percent`. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/3RMUFhcG998" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Safety and fairness in genAI models: how does it impact my development work?

GitHub Copilot's model provider, OpenAI, has made [statements](https://openai.com/index/moving-ai-governance-forward/) about improving the safety, security and trustworthiness of AI. Although I cannot be 100% sure what is behind Copilot's hesitation, it definitely makes sense to have safety measures on certain topics to avoid societal harm. This is especially important when heated words on the internet are dividing our societies or even inciting violence. 

In the example above, the behaviour of Copilot is easily identifiable and understandable. However, as more tasks, and especially higher-level tasks are delegated to genAI in software development, safety and fairness measures also work in less obvious ways. This requires developers, as AI users, to have a strong understanding of how AI safety measures work. As we use Copilot to write codes, don't forget to ask the following questions:

- Does part of my development / analytical project have risks in terms of safety, security, societal harm and fairness?

- Does Copilot seem to behave oddly at part of my project? Could AI safety measures be at play?

- Does Copilot seem to ignore part of your data? Does such data have privacy, safety, ethics or fairness concerns?

## Beyond safety

Safety, security and fairness in AI systems are important and complex topics, which, we as users of genAI, should nonetheless keep in mind. In the example above, Copilot's hesitation mitigates risks due to genAI having a harmful output, but it also creates risks due to **genAI not having a good output**. 

- Will valuable information about disadvantaged groups of people, for example immigrants or transgender individuals, be kept unattended due to AI safety measures? 

- Will projects dedicated to disadvantaged groups of people receive less support from AI due because they are deemed sensitive or risky?

As genAI rapidly becomes more powerful and widely used, these questions will also demand answers. 
