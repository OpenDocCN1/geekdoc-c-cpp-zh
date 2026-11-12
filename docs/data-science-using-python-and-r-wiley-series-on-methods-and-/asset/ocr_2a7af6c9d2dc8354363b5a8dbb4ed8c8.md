```
In [30]: bank_train.loc[0]
Out[30]:
age             56
job        housemaid
marital       married
education      basic.4y
```

Figure 2.6 Python shows us the variable values of the first record in the bank_train data set (first four variables shown).

What if we want to access many records? We will use the .loc attribute and list the records we want to see. If you want the first, third, and fourth rows, use the following code:

```
bank_train.loc[[0, 2, 3]]
```

If, on the other hand, you want the first 10 rows, inclusive, you would use the following code:

```
bank_train[0:10]
```

While we reference the rows by numbers, our columns have names. This means that if we want to specify which variable we want to see, we give its name.

```
bank_train['age']
```

Using one set of brackets and putting the variable name in single quotes returns the entire variable. The code and first four age values are shown in Figure 2.7.

What if we want to see multiple variables? We will use the .loc attribute and list the variables we want to see. If we want to see the age and job variables, we put each of those variable names inside single quotes, inside double brackets, separated by commas.

```
bank_train[['age', 'job']]
```

The output of this command is shown in Figure 2.8.

# 2.2.7 Setting Up Graphics in Python

Before we leave the Python coding section, we need to address one more thing: how to obtain and tweak graphical output in Python.

By default, Spyder shows all graphics in the IPython console in the lower-right window. An example of this is shown in Figure 2.9, using a histogram. These small displays, with no edit options, may be acceptable for simple graphs. However, we are going to be making complex graphics, which will require further editing and a larger display. To enable us to view and manipulate the graphs in detail, we need to change Spyder’s graphics settings.