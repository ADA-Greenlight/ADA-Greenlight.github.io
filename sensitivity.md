---
layout: page
title: Sensitivity Analysis
subtitle: Assessing the bias needed to change the results
---

## 

Concern : violation of the randomized treatment assignment ?
 
Naive model, they assume that the probability to be trated in 0.5 inside the pair treated control.

Sensitivity analysis is a way of quantifying how would the results of our calculations change if the assumptions were violated by a limited amount.
Similar to the ... analysis of dynamical systems. Change the input by a little amount and look at the output.

We measure by how much
that assumption needs to be violated to alter our conclusion that there is a
significant difference in differences effect on the

In treatment-control pairs matched, the chance that the first person in pair p is treated is θ p = 1 / 2 under the assumption that treatment assignment is ignorable. What if that assumption is wrong?

By how much would θ p have to depart from 0.5 to obtain a P-value above 0.05 so that we can no longer reject the hypothesis of no effect?

![gamma](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%20%5Cfrac%7B1%7D%7B%5CGamma%7D%20%5Cleq%20%5Cfrac%7B%5Cpi_k%281-%5Cpi_k%29%7D%7B%5Cpi_l%281-%5Cpi_l%29%7D%20%5Cleq%20%5CGamma%20%7D)

## Amplification of Sensitivity Analysis

The question is now to discuss the possibility of an unobserved covariate. Are there other unmeasured covariates that could have an impact on the outcomes of the models ?

In order to do so, we will need to decompose Gamma into two parameters : ![lambda_delta](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%20%28%20%5CLambda%20%2C%20%5CDelta%20%29%7D). These parameters are defined by : ![decomposition](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%5CGamma%20%3D%20%5Cfrac%7B%5CLambda%20%5CDelta%20&plus;%201%7D%7B%5CLambda%20&plus;%20%5CDelta%7D%20%7D).

Delta : strength of the relationship between the unobserved covariate and the difference in outcomes within the matched
pair

Lambda : strength of the relationship between the unobserved covariate and the difference in probability of being assigned a treatment.


