---
layout: page
title: Sensitivity Analysis
subtitle: Assessing the bias needed to change the results
---

## Sensitivity Analysis

In the paper, naive model. They assume that the probability to be trated in 0.5 inside the pair treated control.
In treatment-control pairs matched, the chance that the first person in pair p is treated is θ p = 1 / 2 under the assumption that treatment assignment is ignorable. What if that assumption is wrong?

Concern : is this naive model true ? Quantify the degree to which this naive model is wrong. 
The models assume that the odds of two similar data points (ie very similar observed covariates) are bounded by a factor Gamma.

![gamma](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%20%5Cfrac%7B1%7D%7B%5CGamma%7D%20%5Cleq%20%5Cfrac%7B%5Cpi_k%281-%5Cpi_k%29%7D%7B%5Cpi_l%281-%5Cpi_l%29%7D%20%5Cleq%20%5CGamma%20%7D)

H_0 : No effect on the model
H_1 : An effect on the model

Under the null hypothesis, increasing Gamma increases the p-value.
What is the smallest Gamma for which p > 0.05 ?
By how much would the probability pi have to depart from 0.5 to obtain a p-value above 0.05 so that we can no longer reject H0 ?

Ex : if p > 0.05 for Gamma > 6, then the odds of being a smoker would need to be 6 times higher for two people with same covariates. Very unlikely.

Sensitivity analysis on the matching of the paper :

* Specify the outcomes that we want to test.
* Using sensitivitymv R library (more specifically senmv function), find the gamma for which the p-value is superior to 0.05. This would allow us to evaluate the robustness of the model towards the bias between the paper assignment and a randomized one.


 


Sensitivity analysis is a way of quantifying how would the results of our calculations change if the assumptions were violated by a limited amount.
Similar to the ... analysis of dynamical systems. Change the input by a little amount and look at the output.

We measure by how much
that assumption needs to be violated to alter our conclusion that there is a
significant difference in differences effect on the






## Amplification of Sensitivity Analysis

The question is now to discuss the possibility of existence of an unobserved covariate. Are there other unmeasured covariates that could have an impact on the outcomes of the models ?

In order to do so, we will need to go further and decompose Gamma into two parameters : ![lambda_delta](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%20%28%20%5CLambda%20%2C%20%5CDelta%20%29%7D). These parameters are defined by : ![decomposition](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%5CGamma%20%3D%20%5Cfrac%7B%5CLambda%20%5CDelta%20&plus;%201%7D%7B%5CLambda%20&plus;%20%5CDelta%7D%20%7D).

For each value of Gamma, we can draw a graph of Delta as a function of Lambda.


Delta : strength of the relationship between the unobserved covariate and the difference in outcomes within the matched
pair

Lambda : strength of the relationship between the unobserved covariate and the difference in probability of being assigned a treatment.


