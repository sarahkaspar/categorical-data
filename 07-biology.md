---
title: "Complications with biological data"
teaching: 10
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- When are Fisher- and Chisquare test not applicable for biological data?
- What are alternative methods?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain overdispersion and how it can lead to false positives.  
- Explain random effects.
- Name some alternative methods.

::::::::::::::::::::::::::::::::::::::::::::::::





## Larger tables

Very often, biological data are more complex than can be captured by a $2\times2$ table. 

For example:

2x4 table


2x2x3 table


Fisher's exact test and the $\chi^2$ test can also be applied to 2D tables with more than two categories in each dimension. 

Interpretation for 2x4 example.

## 3D tables

For higher-dimensional tables, it gets a bit more complicated, because it turns out there are several questions that you could ask, and several assumptions that can be made. 

Two examples
- test for independence across replicates: conditional independence --> cmh


::::::::: challenge
## Discussion
We could easily bring the above scenario down to a classical $2\times2$ table by polling the counts across replicates. 
Why is this approach problematic?

:::::::::::: solution
The replicate might have an effect on the row and column sums. Have a look at the Simpson's paradox.
:::::::::::::::::::
::::::::::::::::::

## Three-way interactions 

Refer to Poisson models


## Additional variance

When we're using Fisher's or $\chi^2$ test, we model the data as having been obtained from a particular sampling scheme, like Poisson, binomial or multinomial sampling. These assume that there is an underlying rate, or probability, at which events occur, and which doesn't vary.
For example, we could say that patients show up at a hospital at an average rate of 16 patients per day ($\lambda=16$), and if we took 5 samples at 5 different days, we'd assume the same Poisson rate for each day. The counts would vary from day to day, but with a variance of $var=\lambda$, which is the expected randomness for a Poisson counting process. See also [the lesson on distributions](https://sarahkaspar.github.io/biostatistics-course/05-Poisson.html).

The problem is, that in biology, we often have experiments where we deal with additional variance that can't be explained by the normal variance that's inherent to Poisson counting. 
For example, if we model read counts from RNA sequencing, it turns out that the (residual) variance is much higher than $\lambda$, because the expression of a particular gene usually depends on more factors than just the experimentally controlled condition(s). It is also influenced by additional biological and possibly technical variance, such that the counts vary considerably between replicates.  

### So what?

What happens if we still analyze these data with methods that assume Poisson variance?
This increases the risk for false positives. Intuitively speaking, the increased variance can produce high counts in one or more of the cells, leading to higher proportions than would be expected by change under the assumption of independence and Poisson sampling. So the Fisher test can mistake noise for a difference in proportions.

### What to do?

First of all, think about the data that you're looking at, and how they were produced. If you have several replicates, you have a chance to estimate the variance in your data. In a typical $2\times2$ table, you just have one count per cell, and a different condition in each cell, so there is no chance to infer the variance from looking at the data. In this case you have to ask yourself, whether it's likely that you're overlooking additional variance, and be aware that the data might not perfectly match the assumptions of your test, so don't over-interpret the p-value that you get -- which is always a good advice.

If you do have several counts per condition, you can consider to model your data using a generalized linear model of the negative binomial family. This is outside the scope of this lesson.











