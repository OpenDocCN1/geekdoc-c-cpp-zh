+   - The cumulative logit model
+   - The adjacent categories model
+   - The continuation ratio model

When the dependent variable has only two categories, all three models reduce to the usual binary logit model.

Of the three, the cumulative logit model—also known as the ordered logit or ordinal logit model—is the most widely applicable, and the one that is most easily used in SAS. The adjacent categories model is also an attractive general approach, but SAS can only estimate the model when the data are grouped. The continuation ratio model is more specialized. It’s designed for situations in which the ordered categories represent a longitudinal progression through stages.

# 6.2 Cumulative Logit Model: Example

The cumulative logit model (McCullagh 1980) could hardly be easier to implement in SAS. Whenever PROC LOGISTIC encounters more than two categories on the dependent variable, it automatically estimates a cumulative logit model. Let’s try it and see what we get. Then we’ll step back and discuss the underlying model.

In Chapter 5 we analyzed data in which the dependent variable was the response to the question, “If you found a wallet on the street, would you (1) keep the wallet and the money, (2) keep the money and return the wallet, or (3) return both the wallet and the money?” Although we treated these response categories as unordered, there’s also an obvious ordering: 1 is the most unethical response, 3 is the most ethical, and 2 is in the middle. To fit a cumulative logit model to these data, we submit the program:

```
PROC LOGISTIC DATA=wallet;
    MODEL wallet = male business punish explain;
RUN;
```

(In case you’ve forgotten, the explanatory variables are described in Section 5.2.) Results are shown in Output 6.1.

The output looks virtually identical to output for a binary logit model, except for something new in the middle: the “Score Test for the Proportional Odds Assumption” table. I’ll explain this in more detail later. For now, it’s sufficient to say that this statistic tests whether the ordinal restrictions are valid, and high p-values are desirable. In this case, we