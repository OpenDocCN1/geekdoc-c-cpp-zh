# AN INTRODUCTION TO R

list(o1, o2, ...) returns a list object that contains the R objects o1, o2, ... that were supplied as its arguments. Data frames are hybrid data structures that possess aspects of both matrices and lists. They are constructed using the data.frame function.

There are a number of data sets that come part of the Standard package. A list of all the ones that are available can be obtained by entering the command data(). To obtain a particular data set setName from the one enter data(setName) at the R prompt. This returns a data frame object that holds the contents of the data set.

R provides two assignment operators = and <-. For our purposes can (and will) be used interchangeably. We will tend to use <- in most programming applications as it clearly conveys the direction of assignment. For example, the commands

```
> data(mtcars)
> carData <- mtcars
> mtcars -> carData
```

loads a R data set mtcars into the workspace and assigns it (twice) to the data frame carData.

There are system names that should be avoided when naming variables or constants. These include c, q, t and F. The q function returns an R session, t transposes a matrix and F are abbreviated versions of the R constants TRUE and FALSE that provides the values for a Boolean variable. The c function is of particular importance and occupies a works role in the R language. The c stands for "concatenate" which is what the function does. It takes a comma separated list of arguments and combines them into a vector. For example,

```
> a <- c(1, 3, pi)
> a
[1] 1.000000 3.000000 3.141593
> class(a)
[1] "numeric"
```

produces a vector of the R class or data type "numeric". Note that all that was necessary for R to print the object was simple to enter its name on the command line. This approach works quite general for matrices and R objects and produces the same results as could be obtained using the R show function i.e. show(a) is equivalent to just entering a on the command line. The u-like functions like head and tail are available for matrices and have the effect of showing the first or last rows of the matrix, respectively.

There is a point worth mentioning the R constants. The T and F options correspond to global variables whose initial values are set to TRUE and FALSE. However, T and F can be assigned to other (either internally or otherwise) that can cause errors and confusion. In contrast, TRUE and FALSE are reserved words whose values cannot be changed. It is safest to use the two choices when writing R.

Another basic function that returns has several arguments. For the example the command seq() which has several special case 1:n and seq(1,n) will have the effect of producing the vector of integers from 1 to n. More generally, seq allows for expressions such as seq(1, n, by = r) which selects every r integer between 1 and n or seq(1, length = r) which would list the r partition points are to break the 1 to n into r subintervals of length. There is noting special about the use of integers here and, for an example, a command such as seq(pi/2, -10*pi, length = 7) would have the intended effect of creating a seen partition for the interval [-10pi, pi/2] that breaks it into six subintervals.

![](bbox=[0.105, 0.895, 0.235, 0.908])