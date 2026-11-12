"yes". We save the record numbers as to.resample, as these are the values we want to resample.

Next, we randomly sample from the values in to.resample.

```
our.resample <- sample(x = to.resample, size = 850,
                           replace = TRUE)
```

The x = to.resample input specifies that we want to sample from the series of record indices we created previously. The size = 850 input specifies how many numbers should be resampled. The replace = TRUE input tells the algorithm to sample with replacement. The output is a series of 850 record indices, sampled from our to.resample vector.

Now we want to get the records whose record numbers are those in our. resample.

```
our.resample <- bank_train[our.resample, ]
```

Use of the bracket notation does the job for us. The number of records in the new data set our.resample is 850, which is the number of records we wanted to resample.

Finally, we need to add the resampled records back onto our original training data set.

```
train_bank_rebal <- rbind(bank_train, our.resample)
```

The rbind() command stands for “row bind,” meaning append two data sets by putting the rows on top of each other. By using rbind() on the original training data bank train and the 850 resampled records in our.resample, we have created our rebalanced data set, which we named train_bank_rebal.

To confirm that the resampling has given the desired amount of rare records, look at the table of response values in our rebalanced data set.

```
t.v1 <- table(train_bank_rebal$response)
t.v2 <- rbind(t.v1, round(prop.table(t.v1), 4))
colnames(t.v2) <- c("Response = No", "Response = Yes");
rownames(t.v2) <- c("Count", "Proportion")
t.v2
```

The result is shown in Figure 5.2. The percent of “yes” responses is approximately 30%, which is the percent of rare records we wanted.

| | Response = No | Response = Yes |
|---|---|---|
| Count | 2767.0 | 1186.0 |
| Proportion | 0.7 | 0.3 |

Figure 5.2 The R table of response values after rebalancing.