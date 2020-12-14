---
layout: page
title: Unmeasured Confounding - Sensitivity Analysis of Treatment Effect
subtitle: Housing, Health and Happiness

---

Due to the lack of random assignment to treatment groups in **observational studies**, omitted variable bias can affect treatment effect estimates. One can therefore question results of regression analyses for such studies, and **sensitivity analysis** allows to quantify the impact of potential **omitted variables**. In the paper 'Housing, Health and Happiness', the matching between treatment and control is not fully transparent, and the lack of sensitivity analysis does not allow to measure its performance. 

In this extension, we propose to conduct a robustness check to verify the matching through a sensitivity analysis for various matching methods, in order to assess the bias needed to change the results significantly. Specifically, a **similar matching as proposed in the paper** and a **propensity score matching** are studied. Finally, analysis of the regressions carried out in the paper for the different matchings can be carried out.

Context : In the paper 'Housing, Health and Happiness', the aim is to measure the impact of replacing dirt floors with cement floors in Mexico, on health and welfare of young children and their mothers. A large-scale program called Piso Firme offered households up to 50m² of cement floor. It was established by the Mexican government in 2000 in the State of Coahuila first then in 2004 in the state of Durango. The study observes the evolution of two populations in two twin cities : Gomez Palacios and Lerdo, State of Coahuila (group control) and Torreon, State of Durango (group treatment). They are geographically close but the beginning of the program implementation differ as they are in two different states. They proceded in three steps : verification that control and treatment groups are well balanced, estimation of the program impact and examination of the robustness of the results. Their verification showed that both control and treatment groups were balanced on all levels before the program. Their conclusion was that the Piso Firme program improved health and welfare of young children and their parents. The cement floors significantly reduced the number of cases of parasitic infestations, diarrhea, anemia and then improved the health and cognitive development of the children. They also increased happiness and quality of life of adults as well as decreased depression.

{% include toc.html html=content %}

### I. The Problems with Observational Studies

## Randomised ? 

In an ideal randomised trial, the treatment assignment would be randomly decided (equivalent to a 50/50 coin flip). Therefore, if we assume the trial is actually randomised, the distribution of our covariates will be the same in both groups, i.e. the covariates are said to be balanced. In this case, the control and treatment groups are indistinguishable. Thus, if the outcome between different treatment groups end up differing, it will not be because of differences in the covariates defining the groups, it will be because of the treatment.

However, as it is not always possible to perform a randomised trial (either unethical, impractical, too expensive, ...), **observational studies** are conducted, where there is no intervention in the treatment assignment and retrospective data is observed. This is the case of the 'Housing, Health and Happiness' paper. Indeed, data is collected from census and surveys a posteriori and the researchers cannot control the conditions under which samples are distributed. This might lead to a potential problem as the decision of which subjects receive the treatment is not entirely random and thus a potential source of bias.

To be more precise, subjects are selected to be treated and the treatment assignment and the outcome may be caused by the same hidden covariate. For observational studies, the distribution of variables will typically differ between treatment and control group, as it is not a randomised trial. The goal of the study is to determine the effects of the variables defining households before the begining of the program on the outcome but sometimes the measured covariates may not be directly causing the differences in the outcome. There might be more covariates which were not measured but are actually important in the chain of cause and effect. These variables that affect both treatment assignment and outcome are called **confounders**. In observational studies, an important assumption in the estimation of causal effect is the **ignorability assumption** : given pre-treatment covariates, treatment assignment is independent of the potential outcome, also known as the "no unmeasured confounders' assumption".  

-> si on veut ajouter des graphes on peut mettre un schéma graphe comme dans le cours pour illustrer l'effet du confounder sur treatment and outcome.


### II. The Solution: Matching and Sensitivity Analysis

## A) Theory and background

## Matching :

To solve the issue of the difference in variables distribution between control and treatment group, **matching** is performed. The idea is to match individuals in the treated group with similar individuals in the control group for the covariates. In the ideal case, we would like to find for each sample in the treatment group, an identical sample in the control group in terms of pre-treatment covariates. This is generally impossible but fortunately, finding similar sample in the control group is enough. The condition is that the two samples in the matched pair have probability of receiving the treatment is as close as possible. 
This is not an exact matching as the paired samples can be slightly diffferent but the overall distribution of each pre-treatment variable is balanced between the groups, this is known as stochastic balance. Matching is a technique that attempts to control for confounding and make an observational study more like a randomised trial. It enables a comparison of outcomes among treated and control samples to estimate the effect of the treatment and reducing the bias due to a potential confounder. Matching can be done in different ways.

## Sensitivity Analysis :

Matching can improve the veracity of the results. It ensures that similar samples are compared, i.e. they are similar in terms of observed variables. Nevertheless, there might be some unobserved covariates that highly differ between the two samples. In other words, a **naive model** assumes that the probability to be trated was 0.5 inside the pairs treated-control. However, there might exists a unmeasured confouder that could unbalance this probability by favouring one sample or the other. **Sensibility analysis** allows to quantify the degree to which the naive model is wrong.  

" In treatment-control pairs matched, the chance that the first person in pair p is treated is θ = 1/2 under the assumption that treatment assignment is ignorable. What if that assumption is wrong ? " citation de Rosenbaum, _Observation and experiment_

The intuition is that the naive model would be wrong if there exists a confouder sufficiently important to modify the probability of being treated by a huge amount. Let's be more precise. The models assumes that the odds of two similar data points (i.e. very similar observed covariates) are bounded by a factor Gamma :
![gamma](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%20%5Cfrac%7B1%7D%7B%5CGamma%7D%20%5Cleq%20%5Cfrac%7B%5Cpi_k%281-%5Cpi_k%29%7D%7B%5Cpi_l%281-%5Cpi_l%29%7D%20%5Cleq%20%5CGamma%20%7D) For example, if Gamma = 3, the odds ratio is comprised between 1/3 and 3, and the probabilty of being treated is comprised between 0.25 and 0.75. 

For each value of Gamma, we use a statistical test with the following hypotheses :
* H_0 : No treatment effect on the model.
* H_1 : A treatment effect on the model.

If p-value < 0.05, we can reject the null hypothesis H_0 of no treatment effect. We start with Gamma = 1 and then increase its value. Under the null hypothesis, increasing Gamma increases the p-value. Finding the smallest Gamma for which p > 0.05 corresponds to finding by how much would the probability have to depart from 0.5 to obtain a p-value above 0.05 so that the hypothesis of no treatment effect cannot be rejected. For example, if we obtain p > 0.05 for Gamma > 6, then the odds of being treated would need to be 6 times higher for two people with same covariates. Therefore, estimating a value for Gamma allows us to evaluate the likelihood of a potential hidden covariate and the consequence of this covariate on the results.

In practice, we use in this work the _sensitivitymv R_ library and more specifically senmv function. This would allow us to evaluate the robustness of the model towards the bias between the paper assignment and a randomized one.


## Amplification of Sensitivity Analysis :

The question is now to discuss the possibility of existence of an unobserved covariate. Are there other unmeasured covariates that could have an impact on the outcomes of the models ?

In order to do so, we will need to go further and decompose Gamma into two parameters : ![lambda_delta](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%20%28%20%5CLambda%20%2C%20%5CDelta%20%29%7D). These parameters are defined by : ![decomposition](https://latex.codecogs.com/gif.latex?%5Cmathbf%7B%5CGamma%20%3D%20%5Cfrac%7B%5CLambda%20%5CDelta%20&plus;%201%7D%7B%5CLambda%20&plus;%20%5CDelta%7D%20%7D).

For each value of Gamma, we can draw a graph of Delta as a function of Lambda.

Delta = shift : strength of the relationship between the unobserved covariate and the difference in outcomes within the matched
pair

Lambda =strength : strength of the relationship between the unobserved covariate and the difference in probability of being assigned a treatment.

## B) Analysis of available data

Check balance prior to matching with SMD for the census variables used for the matching (matching with pre-treatment variables, not with outcomes!)

## C) Replicating the paper's matching method

- In the paper they use an L-infinite norm : the pairs are created based on 4 pre-treatment variables : 
* C_blocksdirtfloor : Proportion blocks of houses with 1+ houses that has dirt floors
* C_HHdirtfloor : Proportion of households with dirt floors
* C_child05 : Average number of children between 0-5 yrs
* C_households : Number of households
They are matching on the observed covaraites. The idea is to minimise the L-infinite distance to match the pairs of control and treatment data points. The L-infinite distance is defined as the maximum of the absolute value of the differences between the variables for each pair of treatment and control blocks. We can compute the L-infinite distance between each possible pair of treated and control data points and minimise to obtain the final matching.

In practice :
- construct bipartite graph : node = sample, treated samples on one hand and control samples on the other hand. 
Edge = links one control and one treated sample, weighted with the L-infinite norm.
- Aim : minimise the norm over the matching. So the algorithms finds the best matched pairs such that the norm is minimum.

The two Figures below allows to visualise the distribution of control and treatment data before and after the matching. No significant difference are observed.

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="90%" height="500" allowfullscreen="true" src="assets/img/boxplot_figure.html"></iframe>

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="100%" height="500" allowfullscreen="true" src="assets/img/ttest_table.html"></iframe>

## D) Propensity score matching

We want that the two samples of the pair have the same probability to be treated pi as defined below. 
-> add formula of pi from the course.
Instead of matching on observed covariates directly, the idea is to reduce the information of all the pre-treatment covariates to one signle number called the propensity score. This number is computed for every samples using a logistic regression. By doing so, the samples with equal propensity score are guaranted to have equal distributions of observed variables. The samples in the same pair might not have equal x but total treatment and control groups will have the same distribution. 

In practice :
- construct bipartite graph : same as explained above for the matching of the paper. Edges weighted with the difference of similarity score. Similarity = 1 - difference of propensity score. 
- we want to minimise the difference of propensity score between the pairs. Equivalently we can maximise the similarity between the pairs. Find the matching that miximises the overall similarity. 


### Regression Analysis : -> à changer de place

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="120%" height="500" allowfullscreen="true" src="assets/img/Bias_Figure_T4.html"></iframe>

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="120%" height="500" allowfullscreen="true" src="assets/img/Bias_Figure_T6.html"></iframe>


### IV. Conclusion

Answer the research questions :
* Most important variables in the data set in terms of predicting power for the studied models : ...
    
* Potential bias to alter the conclusions of the study :
The method of the paper is very sensible to small bias. And even more, by following their method and applying sensitivity analysis, we can put into question their final results.

* Would propensity score matching (or another matching method) improve the accuracy of the results ?
It seems that propensity score improves the results.
Put into question the matching in the study.
Criticise the lack of pre-matching data, as we cannot really verify their matching methods (not fully transparent). Here we can clearly say that their matching is not good but we cannot clearly saying if their results are significant.


### Resources 

 * Paul R. Rosenbaum, _Design of observational studies_, Springer series in Statistics. 2010
 * Paul R. Rosenbaum, _Observation & Experiment : An Introduction to Causal Inference_, Harvard University Press, 2017  
 * Paul R. Rosenbaum, _Sensitivity Analysis in Observational Studies_, Encyclopedia of Statistics in Behavioral Science (Vol.4), 2005
 * C. A. Hosman et al., _The Sensitivity of Linear Regression Coefficients' Confidence Limits to the Omission of a Cofounder_, The Annals of Applied Statistics (Vol.4), 2010
 * Paul R. Rosenbaum, _Package ‘sensitivitymv’_, 2018
 

