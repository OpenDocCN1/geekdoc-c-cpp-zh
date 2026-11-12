
mortgage loans. Similarly, for credit card companies. The classification models are shown lots of complete records containing the actual default status of past customers. The models then learn which attributes are associated with customers who default. Finally, these trained models are then deployed to new data, customers who have applied for a loan or a credit card, with the expectation that the models will help to classify which customers are most likely to default on their loans. Classification methods are covered in Chapters 6, 8, 9, and 13.

### 1.4.4 Clustering

The clustering task seeks to identify groups of records which are similar. For example, in a data set of credit card applicants, one cluster might represent younger, more educated customers, while another cluster might represent older, less educated customers. The idea is that the records in a cluster are similar to other records in the same cluster, but different from the records in other clusters. Finding workable clusters is useful in at least two respects: (i) your client may be interested in the cluster profiles, that is, detailed descriptions of the characteristics of each cluster, or (ii) the clusters may themselves be used as inputs to classification or estimation models downstream. Clustering methods are covered in Chapter 10.

### 1.4.5 Prediction

The prediction task is similar to estimation or classification, except that for prediction the forecasts relate to the future. For example, a financial analyst may be interested in predicting the price of Apple stock three months down the road. This would represent estimation, since price is a numeric variable, and prediction, since it relates to the future. Alternatively, a drug discovery chemist may be interested in whether a particular molecule will lead to a profitable new drug for a pharmaceutical company. This represents both prediction and classification, since the target variable is a yes/no variable, whether the drug will be profitable.

### 1.4.6 Association

The association task involves determining which attributes are associated with each other, that is, which attributes “go together.” The data scientist using association seeks to uncover rules for quantifying the relationship between two or more attributes. These association rules take the form, “If antecedent, then consequent,” together with measures of the support and confidence of the association rule. For example, marketers trying to avoid customer churn might uncover the following association rule: “If calls to customer service greater than three, then customer will churn.” The support refers to the proportion of records the rule applies to; the confidence is the proportion of times the rule is correct. We cover the association task in Chapter 14.

## EXERCISES

## CLARIFYING THE CONCEPTS

- 1. What is data science?
- 2. Which areas of study does data science combine?
- 3. What is the goal of data science?
- 4. Name the seven phases of the DSM.
- 5. Why is it a good idea to have a Problem Understanding Phase?
- 6. Why do we need a Data Preparation Phase? Name three issues that are handled in this phase.
- 7. In which phase does the data analyst begin to explore the data to learn some simple information?
- 8. Explain in your own words why we need to establish baseline performance for our models. Which phase does this occur in?
- 9. Which phase represents the heart of your data scientific investigation? Why might we apply more than one algorithm to solve a problem?
- 10. How do we determine whether our predictions are any good? During which phase does this occur?
- 11. True or false: The data scientist’s work is done with the Evaluation Phase. Explain.
- 12. Explain how the DSM is adaptive.
- 13. Describe how the DSM is iterative.
- 14. List the most common data science tasks.
- 15. Which of these tasks have many nonspecialists been doing all along?
- 16. What is estimation? In estimation, what must be true of the target variable?
- 17. What is the most widespread task in data science? For this task, what must be true of the target variable?
- 18. What are cluster profiles?
- 19. True or false: Prediction can only be used for categorical target variables. Explain.
- 20. For an association rule, what do we mean by support?

## 2.1 DOWNLOADING PYTHON

To run Python code, you need to use a Python compiler. In this text, we will be using the Spyder compiler, which is included in the Anaconda software package. By downloading and installing Anaconda, we will also download and install Python at the same time.

To download Anaconda, go to the Spyder installation page¹ and select the Anaconda link under either the Windows or MacOS X options. After the installation is complete, locate the Spyder program and open it.

When you open Spyder for the first time, you will see the screen shown in Figure 2.1. The left-hand box is where you will write Python code. That box is where we will spend most of our time. The top-right box lists data sets and other items that have been created by running Python code. The bottom-right box is where our output will appear, as well as any error messages or other information.

## 2.2 BASICS OF CODING IN PYTHON

In Python, as in most other programming languages, you run code which performs an action. Some actions also generate output. There are five kinds of actions we will focus on in this chapter: Using comments, Importing packages, Executing commands, Saving output, and Getting data into Python.

### 2.2.1 Using Comments in Python

Comments are pieces of code that are not executed by the compiler. Why are we starting our programming chapter with commands that would not be run? Because comments are a vital part of any programming project.

![](img/fbc96b887811576a0dc93355dce68ae3_23_0.png)

Figure 2.1 The Spyder window when you first open the program.

Comments are lines of code that the programmer puts there for others to understand the code better. For example, if you want to explain what a particular piece of code does, you may begin with a comment that explains what it does and what the result will be.

How do we write comments in Python? Comments are lines of code that start with a pound sign, #. The following is an example of a comment.

```
# This is a comment!
```

Notice that the typeface for any code, even comments, will be given in bold-face in this textbook. This applies to both Python and R code.

### 2.2.2 Executing Commands in Python

Any code you type needs to be run, or executed, before it will work. There are a few different ways to execute code.

Most often, your cursor will be on one line of code, and you will want to run that line. There is a button in Spyder to run a single line of code. There is also a keyboard shortcut, which is revealed if you hover over that button. Both the button and the hover text are shown in Figure 2.2.

You may want to run multiple lines of code at the same time. In that case, highlight the relevant lines and press the “Run selection or current line” button, or press the keyboard shortcut. All highlighted code will be run at the same time.

You can also try executing comments. As discussed previously, comments will not be compiled, and there will be no output. They will, however, appear in the

![](img/fbc96b887811576a0dc93355dce68ae3_24_0.png)

Figure 2.2 The button and hover text for running a selection or line of Python code in Spyder.

bottom-right window of Spyder. This tells you that the Spyder compiler has looked at the comment, even though there is nothing for Spyder to do after reading the comment.

### 2.2.3 Importing Packages in Python

While many things can be done in Python “out of the box,” meaning directly after you download and install it, most of what we want to accomplish requires importing packages. Packages contain specially designed code that will enable us to perform complex data science tasks without writing the code ourselves. For example, in Chapter 6, we need to build a classification and regression tree (CART) model. Instead of figuring out how to build a CART model from scratch, we will import a package that contains that code. Once the package is imported, we can run the code to create a CART model.

Some commands are specialized, such as the MultinomialNB() command in the sklearn.naive_bayes package (see Chapter 10). On the other hand, there are some commands that will be used in every chapter. These are the pandas and numpy packages. To import these packages, you need to type and run the following two lines of code:

```
import pandas as pd
import numpy as np
```

Note that we import the packages using import. What about the as pd and as np afterward? The as code renames the package using a name that we can specify. We rename packages to make working with them easier.

To use the commands contained in the pandas and numpy packages, we will need to state the package names before the command name. For example, in Section 2.2.4, we use the read_csv() command from pandas. To use that command, we would need to type pandas.read_csv(). If you are using a particular command multiple times or using code from a package with a long name, you will end up doing a lot of typing! To save some of that typing, we can give a nickname to the package. In the case above, we rename the pandas package as pd using as pd and rename the numpy package as np using as np. This is how, in Section 2.2.4, we can use the read_csv() command using the code pd.read_csv(). Renaming packages will save us a lot of typing in the long run!
