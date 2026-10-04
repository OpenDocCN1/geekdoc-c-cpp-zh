+   d. In Section 4.2.4, you stored the following string:
  R> bar <- "How much wood could a woodchuck chuck"
  i. Store a new string by gluing onto bar the words
     "if a woodchuck could chuck wood".
  ii. In the result of (i), replace all instances of wood with metal.
ne. Store the string "Two 6-packs for $12.99". Then do the following:
  i. Use a check for equality to confirm that the substring
     beginning with character 5 and ending with character 10
     is "6-pack".
  ii. Make it a better deal by changing the price to $10.99.

# 4.3 Factors

In this section, you'll look at some simple functions related to creating, handling, and inspecting factors. Factors are R's most natural way of representing data points that fit in only one of a finite number of distinct categories, rather than belonging to a continuum. Categorical data like this can play an important role in data science, and you'll look at factors again more detail from a statistical perspective in Chapter 13.

# 4.3.1 Identifying Categories

To see how factors work, let's start with a simple data set. Suppose you find eight people and record their first name, sex, and month of birth in Table 4-4.

Table 4-4: An Example Data Set of Eight Individuals

| Person | Sex | Month of birth |
|---|---|---|
| Liz | Female | April |
| Jolene | Female | January |
| Susan | Female | December |
| Boris | Male | September |
| Rochelle | Female | November |
| Tim | Male | July |
| Simon | Male | July |
| Amy | Female | June |