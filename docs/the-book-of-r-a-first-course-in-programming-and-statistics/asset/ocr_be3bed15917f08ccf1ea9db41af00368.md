# 11.3.3 Recursive Functions

Recursion is when a function calls itself. This technique isn’t commonly used in statistical analyses, but it pays to be aware of it. This section will briefly illustrate what it means for a function to call itself.

Suppose you want to write a function that takes a single positive integer argument n and returns the corresponding nth term of the Fibonacci sequence (where n = 1 and n = 2 correspond to the initial two terms 1 and 1, respectively). Earlier you built up the Fibonacci sequence in an iterative fashion by using a loop. In a recursive function, instead of using a loop to repeat an operation, the function calls itself multiple times. Consider the following:

```
myfibrec <- function(n){
    if(n==1||n==2){
        return(1)
    } else {
        return(myfibrec(n-1)+myfibrec(n-2))
    }
}
```

The recursive myfibrec checks a single if statement that defines a stopping condition. If either 1 or 2 is supplied to the function (requesting the first or second Fibonacci number), then myfibrec directly returns 1. Otherwise, the function returns the sum of myfibrec(n-1) and myfibrec(n-2). That means if you call myfibrec with n greater than 2, the function generates two more calls to myfibrec, using n-1 and n-2. The recursion continues until it reaches a call for the 1st or 2nd term, triggering the stopping condition, if(n==1||n==2), which simply returns 1. Here’s a sample call that retrieves the fifth Fibonacci number:

```
R> myfibrec(5)
[1] 5
```

Figure 11-3 shows the structure of this recursive call.
Note that an accessible stopping rule is critical to any recursive function. Without one, recursion will continue indefinitely. For example, the current definition of myfibrec works as long as the user supplies a positive integer for the argument n. But if n is negative, the stopping rule condition will never be satisfied, and the function will recur indefinitely (though R has some automated safeguards to help prevent this and should just return an error message rather than getting stuck in an infinite loop).

Recursion is a powerful approach, especially when you don’t know ahead of time how many times a function needs be called to complete a task. For many sort and search algorithms, recursion provides the speediest and most efficient solution. But in simpler cases, such as the Fibonacci example here, the recursive approach often requires more computational expense than an iterative looping approach. For beginners, I recommended sticking with explicit loops unless recursion is strictly required.