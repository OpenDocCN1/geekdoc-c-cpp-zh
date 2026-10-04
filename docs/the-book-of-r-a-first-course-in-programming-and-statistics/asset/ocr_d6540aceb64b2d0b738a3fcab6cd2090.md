The differences between this version and multiples1 are in the first and last if statements. The first statement checks whether there are no matrices in x, in which case it returns a string message. In multiples1, that message was always stri, but now you use another statement with missing(stri) argument that has a value first. If not, the function returns another character string saying that stri was missing. A similar alternative is defined for str2. Here it is once more importing the function and using foo, bar, and baz:

```
R multiples3(foo,diag(2))
[[1]]
[,1] [,2]
[1,] 1 3
[2,] 2 4

[[2]]
[,1] [,2]
[1,] 1 5
[2,] 2 6
[3,] 3 7
[4,] 4 8

R multiples3(bar,diag(2))
[1] "stri" was missing, so this is the message
R multiples3(baz,diag(2))
[1] "str2" was missing, so this is the message
```

Using this way permits arguments to be left unspecified in a given function call. It is primarily used when it's difficult to choose a default value for a certain argument, yet the function still needs to handle cases when argument is not provided. In the current example, it makes more sense to define defaults for stri and str2, as you did for multiples2, and avoid the extra code required to implement missing.

# 11.2.4 Dealing with Ellipses

In Section 9.2.5, I introduced the ellipse, also called dot-dot-dot notation. The ellipsis allows you to pass in arguments without having to first define them in the argument list, and these arguments can then be passed to another function call within the code body. When included in a function definition, the ellipse is often (but not always) placed in the last position because it represents a variable number of arguments.

Building on the fib3 function from Section 11.1.1, let us use the ellipse to plot the specified Fibonacci numbers.

```
myfibplot <- function(thresh,plot=TRUE,...)
  fibseq <- c(1,1)
  counter <- 2
```