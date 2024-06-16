---
title: "It does not look like a Shiny App! Use GitHub Copilot to generate custom Shiny UI"
date: 2024-6-14
tags: [Shiny, UI, GitHub Copilot]
header:
excerpt: "Shiny, artificial intelligence, large language models, user interface"
---

Powerful tool as it is, R Shiny is typically not the only front-end framework that an organization uses. Often times, organizations use popular frameworks like React and Angular to create the majority of user interfaces, and use R Shiny to present and let users interact with data. Naturally, this discrepancy in frameworks creates challenges, as a consistent UI design across a company's online presence is key to promoting a strong brand identity. 

Additionally, Shiny developers tend to be R users and come from a data analytics background. They may not have the strongest expertise in front-end tools such as HTML and CSS. Creating the appropriate classes for Shiny elements and defining their attributes usually end up being daunting and frustrating tasks that do not add much value to the work of a data specialist. 

With the help of GenAI-backed programming tools such as GitHub Copilot, front-end developers can easily create Shiny UIs that match the overall aesthetic style of other web assets. Here, I will demonstrate how I re-created the front-page of my [personal blog site](https://zibowangkangyu.github.io/), which was initially created using Jakyll, as the UI page of an R Shiny app in no time. As a result, R Shiny developers will be able to insert data tabulations, visualizations and all kinds of interactive elements into a dashboard that does not look like a Shiny app, but a Jakyll blog site. 

## Some tips of interacting with GitHub Copilot

If you use genAI tools, you have probably learned some tricks that help the AI generate the most useful and accurate context. I would highly recommend the short course by Microsoft [here](https://learn.microsoft.com/en-us/training/paths/copilot/) for those who want to dig deeper into how Copilot works. In the context of R and Shiny programming, I try to pay attention to two simple elements to receive quality suggestions from Copilot: context and prompts. 

Context and prompts can mean different things in the world of genAI, or both users and developers of large language models (LLMs). I find it helpful to think of context as something you would write as descriptive sentences, for example: 

- This file is part of an R Shiny app that analyzes the demographic compositions of cities in the Greated Toronto Area. The Shiny app should look the same as the existing webpage stored in `index.html`, which is the front page of my personal blog.

On the other hand, prompts are usually written as command sentences, for example: 

- Test that the `summarize_immigrant_percentage` function returns a tibble.   

### Set the context

Although the latest GPT model is said to have been trained on more than 10 trillion (1 followed by 13 0s) tokens (roughly mean words), it still needs to know what is important to you. The best way to set the right context is to show Copilot content relevant to your goals, be it in human language or code. If you use RStudio or its cloud versions, there are three ways to do it:

- Put the most important context in the currently active tab, even it means we delete it later afterwards. For example, we need to put the Shiny UI code in the `app.R` file for the Shiny app to run. However, since the target code is closely related to `index.html` (we are essentially asking Copilot to translate the html code into R), I would copy and paste the whole html file into `app.R` so that Copilot knows that this is the most important chunk of code. We can easily delete the HTML code after Copilot finishes its job. 

```{r}
# Above is the index.html file. The file is a template for a website's homepage.
# Now, I want to re-create the homepage, but with R Shiny.

# [INSERT HTML CODE ...] #
```
- Open the other important files in your IDE. Copilot uses a [technique](https://github.blog/2023-05-17-how-github-copilot-is-getting-better-at-understanding-your-code/#how-github-copilot-understands-your-code) called "Neighboring tabs", which lets it process all of the files open in a developer’s IDE. In the context of this specific task, it makes sens to keep the following files open in RStudio: `assets/css/main.scss` and `assets/js/main.min.js`. Why? Because these are local files that are directly referred to in `index.heml`. Use your own judgement to decide what files are the 

- Create R Project and allow "Index project files with GitHub Copilot" in Copilot settings. This choice is given when you first enable Copilot in RStudio. After creating an R Project, Copilot will use all files in the project folder as context.

<img src="{{ site.url }}{{ site.baseurl }}/images/copilot_ui/plots/allow_index.png" alt="Allow index project files">

### Write good prompts

Prompt engineering has rapidly become a must-have skill for genAI users, and there are plenty of resources online on writing effective prompts. According to Microsoft, prompt engineering should follow such [principles](https://learn.microsoft.com/en-us/training/modules/introduction-prompt-engineering-with-github-copilot/2-prompt-engineering-foundations-best-practices) as: 

- Single: Always focus your prompt on a single, well-defined task or question, instead of multiple tasks.
- Specific: Ensure that your instructions are explicit and detailed. 
- Short: While being specific, keep prompts concise and to the point.

As an example, the following is the prompt I wrote.

```{r}
# [INSERT HTML CODE ...] #
# Above is the index.html file. It is my website's homepage.
# Now, Re-create the homepage, but with R Shiny.
# The UI portion of the Shiny app will be the same as the index.html file.
```

The first line summarizes the most important context in this task: the existing html file. 
The second and third lines of my prompt specify the main task that I expect Copilot to do for me: re-create the home page, and: 

- Do it with R Shiny.

- Make it look like the existing html file. 

## Refer to tool-specific knowledge on the internet

Although Copilot and the underlying GPT model should have "learned" almost all knowledge available on the internet, it is still useful to point to the most relevant resources on the internet. As a human programmer, if you are given the task to create this Shiny UI, which resources would you start with? For this example, this [Shiny HTML Tags Glossary](https://shiny.posit.co/r/articles/build/tag-glossary/) contains almost all information needed. I added the following to the prompt: 

```{r}

# Refer here: https://shiny.posit.co/r/articles/build/html-tags/
# for more information on how to convert HTML to Shiny.

```

## Provide Copilot with examples

To make the task more tangible for Copilot, I also provided a few examples. Again, think from a human developer's perspective, what do I need to do to to convert html code to R Shiny?

```{html}
<h3 class="author__name" itemprop="name">Mark Wang</h3>
```

```{r}
tags$h3(class = "author__name", itemprop = "name", "Mark Wang")
```

For code translation, we are essentially make two changes: 

- Tag translation, from `<h3>` to `tags$h3`.

- Attribute translation, for `class` and `itemprop`

Add the following to tell Copilot to do exactly this:

```{r}

# For example, the "h2" tag in HTML is equivalent to "tags$h2" in Shiny.
# The "html" tag in HTML is equivalent to "tags$html" in Shiny.

# Also, tag attributes in HTML are passed as arguments in Shiny.
# For example, the "class" attribute in HTML is passed as "class = " in Shiny.
# The "lang" attribute in HTML is passed as "lang = " in Shiny.
```

## Assert and iterate 

Copilot does not always give the best code recommendation, especially when the "correct" output is as long as 124 lines. Luckily, the first iteration already renders pretty good results: 

