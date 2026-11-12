specifying ascending = False. We can save this sorted data set under its own name, say bank_train_sort.

Finally, let us say we want to report the age and marital status of the 15 people who have the largest age_z values. This condition specifies both the number of rows to report (15) and the columns to report (the variables named age and marital).

```
bank_train_sort[['age', 'marital']].head(n=15)
```

The double-bracket notation given after the data set name lets us specify which columns to include. The head() command will give the top records, stopping after n records if n is given, or after five records if no n value is given. In our case, we specify n = 15. The results are the age and marital status of the people with the 15 largest age_z values.

# 3.8.2 How to Identify Outliers Using R

For this example, we will continue using the age_z variable that we created in the previous section. We can isolate individual records using bracket notation detailed in the previous chapter. The structure of our code will begin as follows:

```
bank_train[ rows of interest, ]
```

Note that the right-hand side of the comma is left blank. As we have not specified any columns of interest, all columns will be returned in the output of this command.

We now need to fill in which rows we are interested in. The which() command will identify the records that meet specified conditions.

```
bank_outliers <- bank_train[ which(bank_train$age_z < -3 | bank_train$age_z > 3), ]
```

The condition given as the input to the which() command states that we want all records whose age_z values are less than -3 or greater than 3. The which() command returns the row indices of all such records. The bracket notation will return a subset of the bank_train data set that holds only those records. We can save those records as a new data set, bank_outliers.

To sort a data set by a variable, we use the order() command.

```
bank_train_sort <- bank_train[ order(- bank_train$age_z), ]
```

The order() command takes as input a variable to be sorted. It returns the row indices of the variable after it has been sorted. By default, the values are sorted in ascending order. To sort instead by descending order, we add a minus sign in front of the variable, as shown.