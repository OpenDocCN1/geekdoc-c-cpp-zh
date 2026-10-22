# Chapter 5

# Multinomial Logit Analysis

+   5.1  Introduction  139
+   
+   5.2  Example  140
+   
+   5.3  A Model for Three Categories  141
+   
+   5.4  Estimation with PROC LOGISTIC  143
+   
+   5.5  Estimation with a Binary Logit Procedure  152
+   
+   5.6  General Form of the Model  153
+   
+   5.7  Contingency Table Analysis  154
+   
+   5.8  Problems of Interpretation  157

# 5.1  Introduction

Binary logistic regression is ideal when your dependent variable has two categories, but what if it has three or more? In some cases, it may be reasonable to collapse categories so that you have only two, but that strategy inevitably involves some loss of information. In other cases, collapsing categories could seriously obscure what you’re trying to study. Suppose you want to estimate a model predicting whether newly registered voters choose to register as Democrats, Republicans, or Independents. Combining any two of these outcomes could lead to seriously misleading conclusions.

How you deal with such situations depends somewhat on the nature of the outcome variable and the goal of the analysis. If the categories of the dependent variable have an inherent ordering, the methods in the next chapter should do the job. If there’s no inherent ordering and the goal is a model in which characteristics of the outcome categories predict