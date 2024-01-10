# MIQP-vs-LASSO-Optimal-Variable-Selection-Strategies

## Problem Overview
One of the most common problems in predictive analytics is variable selection for regression. Direct variable selection using optimization has long been dismissed by the statistics/analytics community because of computational difficulties. This computational issue was part of the motivation for the development of LASSO and ridge regression. However, in the recent past there have been tremendous advancements in optimization software, specifically the ability to solve mixed integer quadratic programs (MIQP). This project will pose the variable selection problem for regression as an MIQP which you will solve using gurobi. We will compare the results you find to LASSO to see if the additional ‘shrinkage’ component of LASSO really is more beneficial than finding the ‘best’ set of variables to include in your regression.

## Direct Variable Selection – MIQP Problem
Given a dataset of m independent variables, X, and a dependent variable, y, the standard ordinary least squares problem is formulated as min𝛽Σ(𝛽0+𝛽1𝑥𝑖1+⋯+𝛽𝑚𝑥𝑖𝑚−𝑦𝑖)2𝑛𝑖=1.
In order to incorporate variable selection into this problem we can include some binary variables, zj, that force the corresponding values of 𝛽𝑗 to be zero if zj is zero, using the big-M method that we discussed in class, and used in the previous project. If we only want to include at most k variables from X, then we can pose this as min𝛽,𝑧Σ(𝛽0+𝛽1𝑥𝑖1+⋯+𝛽𝑚𝑥𝑖𝑚−𝑦𝑖)2𝑛𝑖=1 𝑠.𝑡.−𝑀𝑧𝑗≤𝛽𝑗≤𝑀𝑧𝑗 𝑓𝑜𝑟 𝑗=1,2,3,…,𝑚 Σ𝑧𝑗𝑚𝑗=1≤𝑘 𝑧𝑗 𝑎𝑟𝑒 𝑏𝑖𝑛𝑎𝑟𝑦.
Note that we don’t ever forbid the model from having an intercept term, 𝛽0, and that m and M are different things here. Here, k can be viewed as a hyperparameter to be chosen using cross validation.

## Indirect Variable Selection – LASSO
The LASSO version of regression is posed as min𝛽Σ(𝛽0+𝛽1𝑥𝑖1+⋯+𝛽𝑚𝑥𝑖𝑚−𝑦𝑖)2𝑛𝑖=1+𝜆Σ|𝛽𝑗|𝑚𝑗=1,
where 𝜆 is a hyperparameter to be chosen using cross-validation. It turns out that if 𝜆 is large enough, several values of 𝛽 will be forced to be equal to zero. This model also has the benefit of ‘shrinking’ the 𝛽s closer to zero, which achieves variance reduction (prevents overfitting). Note again that 𝛽0 is not included in the 𝜆 sum. You should never penalize a model for having an intercept term. The standard package in Python to solve the LASSO problem is scikit learn. In this project you will need to use scikit learn to solve the LASSO problem.
