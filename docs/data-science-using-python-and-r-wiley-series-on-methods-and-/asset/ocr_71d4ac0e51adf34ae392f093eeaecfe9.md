To create the index, we first need to find the number of records and columns in the data set.

```
bank_train.shape
```

Using .shape after the name of the data set will give us the number of rows and columns in the data set. The first number in the output is the number of records, 26,874. The second is the number of variables.

Once we know the number of records, we create a new variable that assigns every record a unique integer.

```
bank_train['index'] = pd.Series(range(0,26874))
```

The nested commands Series() and range() create a string of numbers whose lower bound is zero and upper bound is the number of records. Since the Series() command is contained in the pandas package, and we renamed the pandas package pd, we preface the Series() command with pd and a period. The result is the code pd.Series(). Note that the lower bound of the range() command is zero and not one, as Python begins counting locations at zero. We save the series of numbers as a new variable in the data set, index, by assigning the output of pd.Series(range()) to the index variable of the bank_train data set using bank_train['index'].

To view the data set with its new variable, we can look at the head of the data set.

```
bank_train.head
```

Using .head after the name of the data set will generate output containing the first and last 30 records for every variable in the data set.

# 3.4.2 How to Add an Index Field Using R

Import the data set under the name bank_train, using the Import Dataset button in RStudio. To create an index field, we first need to know how many records are in the data set.

```
n <- dim(bank_train)[1]
```

The dim() command gives the number of records and the number of variables for the data set whose name is used as the input value; in this case, the bank_train data set. Adding [1] at the end of dim(bank_train) will result in only the first number, the number of records, being given as the output. We save the output as a lowercase letter “n,” which is the commonly used notation for sample size. If you execute n by itself, the output will be the number 26,874, which is the number of records in the data set.