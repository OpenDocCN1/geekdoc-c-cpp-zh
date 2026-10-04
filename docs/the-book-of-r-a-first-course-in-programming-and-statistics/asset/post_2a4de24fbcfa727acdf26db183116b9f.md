
Meanwhile, if you pass a function to try and it doesn't throw an error, then try has no effect, and you simply get the normal return value.

```
R> attempt2 <- try(myfibrec2(6),silent=TRUE)
R> attempt2
[1] 8
```

Here, you executed myfibrec2 with a valid argument, n=6. Since this call doesn't result in an error, the result passed to attempt2 is the normal return value from myfibrec2, in this case 8.

# Using try in the Body of a Function

Let's see a more complete example of how you could use try in a larger function. The following myfibvector function takes a vector of indexes as the argument nvec and provides the corresponding terms from the Fibonacci sequence:

```
myfibvector <- function(nvec)
nterms <- length(nvec)
result <- rep(0,nterms)
for(i in 1:nterms){
  result[i] <- myfibrec2(nvec[i])
}
return(result)
```

This function uses a for loop to work through nvec element by element, computing the corresponding Fibonacci number with the earlier function, myfibrec2. As long as all the values in nvec are nonzero, myfibvector works just fine. For example, the following call obtains the first, second, tenth, and the eighth Fibonacci number:

```
R> foo <- myfibvector(nvec=c(1,2,10,8))
R> foo
[1] 1 55 21
```

Suppose, there's a mistake and one of the entries in nvec up being zero.

```
R> bar <- myfibvector(nvec=c(3,2,7,0,9,13))
Error in myfibrec2(nvec[1]) : 'n' is uninterpretable at 0
```

The internal call to myfibrec has thrown an error when it's called on n=0, and this has terminated execution of myfibvector. Nothing is returned, and the entire call has failed.

You can prevent this outright by using try within the loop to check each call to myfibrec and have it catch any errors. The following function, myfibvectorTRY, does just that.

```
myfibvectorTRY <- function(nvec){
  nterms <- length(nvec)
  result <- rep(0,nterms)
  for(i in 1:nterms) {
    attempt <- try(myfibrec2(i]),silent=T)
    if(class(attempt)==="try-error"){
      result[i] <- NA
    } else {
      result[i] <- attempt
    }
  }
  return(result)
}
```

Here, within the for loop, use attempt to store the result of trying each call to myfibrec2. Then, inspect attempt. If this object's class is "try-error", that means myfibrec2 produced an error, and you fill the corresponding slot in the result vector with NA. Otherwise, attempt will represent a valid value from myfibrec2, so you place it in the corresponding slot of the result vector. Now if you import and call myfibvectorTRY on the same nvec, you see a complete set of results.

```
R baz <- myfibvectorTRY(nvec=c(3,2,7,0,9,13))
R baz
[1] 2 1 13 NA 34 233
```

> The error that would have terminated everything was silently caught, and the alternative response in this situation, NA was inserted into the result vector.

NOTE The command is a simplification of R's more complex tryCatch function, which is beyond the scope of this book, but it provides more precise control over how you test and execute chunks of code. If you're interested in learning more, enter ?tryCatch in the console.

## Suppressing Warning Messages
In all calls I've shown so far, I've set the silent argument to TRUE, which stops any error messages from being printed. If you leave silent to FALSE (the default value), the error message will be printed, but the error will be caught without terminating execution.
Note that silent=TRUE only suppresses error messages, not warnings. Observe the following:

```
R> attempt3 <- try(myfibrec2(-3),silent=TRUE)
Warning message:
In myfibrec2(-3) :
```

Assuming you meant 'n' to be positive -- doing that instead
R> attempt3
[1] 2

Although silent TRUE, the warning (for negative values of n in this sample) is still issued and printed. Warnings are treated separately from errors in this situation, as they should be—they highlight other unforeseen issues with your code during execution. If you are absolutely sure you don't want to see any warnings, you can use suppress.

```
R> attempt4 <- suppressWarnings(myfibrec2(-3))
R> attempt4
[1] 2
```

The suppressWarnings function should be used only if you are certain that every element in a given call can be safely ignored and you want to keep the output tidy.

# Exercise 12.1

- a. In Exercise 11.3 (b) on page 238, your task was to write a recursive R function to compute integer factorials, given some supplied non-negative integer x. Now, modify your function so that it throws an error (with an appropriate message) if x is negative. Test your new function using the following:
  - i. x as 5
  - ii. x as 8
  - iii. x as -8
- b. The idea of matrix inversion, briefly discussed in Section 3.6, is possible only for square matrices (those with an equal number of columns as rows). These inversions can be computed using solve function, for example:

```
R> solve(matrix(1:4,2,2))
     [,2]
[1,]    2 -1
[2,] -1  0.5
```

Note that solve throws an error if the supplied matrix cannot be inverted. With this mind, write an R function that attempts to invert each matrix in a list, according to the following guidelines:
- The function should take four arguments:
- The list x whose members are tested for inversion
- A value to fill in results where a given member of x cannot be inverted, defaulting to NA
- A character string mat to be the result if a given member of x is not a matrix, defaulting to "not a matrix"
- A logical value silent, defaulting to TRUE, to be passed to try in the body
- The function should first check whether x is a list. If not, it should throw an error with an appropriate message.
- Then, the function should ensure that x has at least one member. If not, it should throw an error with an appropriate message.
- Next, the function should check whether mat is a character string. If not, it should coerce it to a character string using an appropriate as.function (see Section 6.2), and it should issue an appropriate warning.
- After these checks, a loop should search each member of x.
- If i is a matrix, attempt to invert it. If it's invertible without error, overwrite member x with the result. If an error is caught, then member of x should be overwritten with the value NA.
- If i is not a matrix, then member of x should be overwritten with the value mat.
- Finally, the modified list x should be returned.

Now, test your function using the following argument:
- i. x as
```
list(1:4,matrix(1:4,1,4),matrix(1:4,4),matrix(1:4,2,2))
```
and all other arguments at default.
- ii. x as Inf, mat as Inf, silent as default.
- iii. Repeat (ii), but now with silent=FALSE.
- iv. x as
```
list(diag(9),matrix(c(0,2,0.4,0.2,0.1,2),3,3),cbind(c(5,1,5,2),c(2,2,1,8)),as.vector(diag(2)))
```
and mat as "unsuitable matrix"; all other values at default.

Finally, test the error messages by calling your function with the following: own- v. x as "hello"
- vi. x as list()

# 12.2 Progress and Timing

R is often used for lengthy numeric exercises, such as simulation or random variate generation. For these complex, time-consuming operations, it is often useful to keep track of progress or see how long a certain task took to complete. For example, you may want to compare the speed of two different programming approaches to a problem. In this section, you'll look at ways to time code execution and show its progress.

## 12.2.1 Textual Progress Bars: Are We There Yet?

A progress bar shows how far along R is as it executes a set of operations. To show this, you need to run code that takes a while to execute, which will be by making R sleep. The Sys.sleep command makes R pause for a specified amount of time, in seconds, before continuing.

```
Sys.sleep(3)
```

If you run this code, R will pause for three seconds before you can continue the code. Sleeping will be used in this section as a surrogate for the delay caused by computationally expensive operations which is where progress bars are most useful.

To use Sys.sleep in a more common fashion, consider the following:

```
sleep_test <- function(n){
  result <- 0
  for(i in 1:n){
    result <- result + 1
    Sys.sleep(0.5)
  }
  return(result)
}
```

The sleep_test function is basic—it takes a positive integer n and adds 1 to the result value for n iterations. At each iteration, you also tell the loop to sleep for a half second. Because of that sleep command, executing the following code takes about four seconds to return a result:

```
sleep_test(8)
[1] 8
```

Now, say you want to track the progress of this type of function as it executes. You implement with three steps: initialize the bar object with txtProgressBar, update the bar with txtProgressBar, and terminate the bar with close. The next function, prog_test, modifies sleep_test to include those three commands.
