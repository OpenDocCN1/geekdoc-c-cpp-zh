# Recursion for Iteration

example. The last section was all about examples pulled from mathematics. The title of this chapter though is recursion for iteration. This is a broader programming concept than the mathematical functions we have talked about. So let us use an example that is very specific to programming.

A simple example to start is with a function that will "count" down from a number to zero. By count here we will print out the values, these functions have side effects. The factorial, we will pass in a single number, the number we want to count down from zero. We also have to have a base case, the point where we stop counting. Since we are counting down to zero, if the value is below zero we are done and should not print anything.

In the recursive case we will have a value, n, that is greater than equal to zero. We definitely want to print n. The question is, what do we do after that? Well, if we are counting down, following n we want to count down then begins with n-1. Indeed, this is how you should imagine the recursion working. Counting down from n is done by counting n, then counting down from n-1. Converting this into code looks like the following:

```
def countDown(n:Int):Unit = {
  if (n<=0) {
    println(n)
    countDown(n-1)
  }
}
```

The code is written, the base case does nothing so we have an if statement that will cause the function to finish without doing anything if the value of n is less than 0. You can call this function passing in different values for n to verify that it works.

Now let us try something different. What if I want to count from one value to another? In some ways, this function looks very much like what we already wrote. There are differences though. In the last function we were always counting down to zero so the only information we needed was what we were counting. In this case, we need to tell both what we are counting from and what we are counting to. That means our function needs two parameters in fact. A recursive cut at this might look like the following:

```
def countFrom(from:Int,to:Int):Unit = {
  if (from>to) {
    countFrom(from-1,to)
  }
}
```

This function will work fine under the assumption that we are counting up. However, if we call with the intention of counting down so that from is bigger than to, you have a problem. To see why, let us trace through this function. First, let us see what happens if we call it with 2 and 5, so we are trying to count from 2 to 5. What we are doing is referred to as tracing the code. It is the act of running through code to see what it does. The substitution method effectively does when we have no side effects, but printing is a side effect, so we need to run the code in a different way to make certain we get the right behavior. This is an essential ability for any programmer. After all, how you write code to complete a given task if you are not able to understand what the code will do? There are lots of different approaches to tracing. Many tables where you write down the values of different variables. Recursive functions you often just write down each call and what it does, then show the calls it makes. That is what we will