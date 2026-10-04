This creates a new age.mon column with the dollar operator and at the same time assigns it the vector of ages in years (already stored as age) multiplied by 12.

# 5.2.3 Logical Record Subsets

In Section 4.1.5, you saw how to use logical flag vectors to subset data structures. This is a particularly useful technique with data frames, where you'll often want to examine a subset of entries that meet certain criteria. For example, when working with data from a clinical drug trial, a researcher might want to examine the results for just male participants and compare them to the results for females. Or the researcher might want to look at the characteristics of individuals who responded most positively to the drug.

Let’s continue to work with mydata. Say you want to examine all records corresponding to males. From Section 4.3.1, you know that the following line will identify the relevant positions in the sex factor vector:

```
R> mydata$sex=="M"
[1] TRUE FALSE FALSE TRUE TRUE TRUE
```

This flags the male records. You can use this with the matrix-like syntax you saw in Section 5.2.1 to get the male-only subset.

```
R> mydata[mydata$sex=="M", ]
  person age sex funny age.mon
1 Peter  42  M High    504
4 Chris  14  M Med     168
5 Stewie  1  M High     12
6 Brian   7  M Med      84
```

This returns data for all variables for only the male participants. You can use the same behavior to pick and choose which variables to return in the subset. For example, since you know you are selecting the males only, you could omit sex from the result using a negative numeric index in the column dimension.

```
R> mydata[mydata$sex=="M",-3]
  person age funny age.mon
1 Peter  42 High    504
4 Chris  14 Med     168
5 Stewie  1 High     12
6 Brian   7 Med      84
```

If you don’t have the column number or if you want to have more control over the returned columns, you can use a character vector of variable names instead.