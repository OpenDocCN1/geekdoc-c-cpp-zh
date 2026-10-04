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