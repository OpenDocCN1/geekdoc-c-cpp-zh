Despite these difficulties, there are situations in which it is easy to fit the loglinear model but difficult to fit the corresponding logit model. One such model is the adjacent-categories model that we considered in Chapter 6. Recall that the adjacent-categories model is one of three alternative logit models for dependent variables with multiple, ordered categories. If the dependent variable has J ordered categories, the model says that for individual i:

log(p_ij / p_i,j+1) = α_j + βx_i      j = 1,...,J − 1

In other words, if we contrast adjacent categories of the dependent variable, the effect of the independent variables on their relative odds is the same regardless of which pair we consider.

This model is a special case of the multinomial logit model that does not impose any ordering on the categories of the dependent variable. (We get the general model by putting a j subscript on the β coefficient.) In Chapter 6, we saw how we could estimate the adjacent categories model in PROC CATMOD by the method of weighted least squares. But the maximum likelihood algorithm in CATMOD cannot impose the necessary constraints on the multinomial model.

Now, we’ll see how to easily estimate the adjacent categories model as a loglinear model by maximum likelihood. In Chapter 6, we looked at the effect of calendar year (1974, 1984, 1994) and marital status (married, unmarried) on reported happiness (very happy=1, pretty happy=2, not too happy=3). Section 6.1 displays the contingency table and the SAS code for reading in the data. But we need to modify the data set as follows:

```
DATA happy2;
    SET happy;
    happyq=happy;
RUN;
```

In this DATA step, I defined a new variable HAPPYQ to be identical to HAPPY, the three-category dependent variable. By defining two versions of the dependent variable, we can treat it as both quantitative and qualitative in the same model. The model is specified as follows:

```
PROC GENMOD DATA=happy2;
    CLASS year happy;
    MODEL count=year|married happy year*happyq married*happyq /
        D=P;
RUN;
```