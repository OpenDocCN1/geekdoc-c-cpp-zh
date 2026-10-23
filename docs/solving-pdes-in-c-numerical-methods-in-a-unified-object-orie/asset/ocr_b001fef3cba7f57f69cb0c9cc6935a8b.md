function to complete it. The computer automatically allocates the required memory for the arguments and the returned value in this recursive call.

The recursive call can by itself use a further recursive call with an even smaller argument "exp". This nested process continues until the final recursive call, which uses a zero "exp" argument, is reached, in which case no further recursive calls are made.

The extra memory allocations for arguments and output make the above recursive implementation of the "power" function less efficient than the original one. This overhead, however, is negligible when large complex objects are implemented. Recursion is invaluable in complex unstructured applications, as we'll see later on.

Next, we use recursion to rewrite the "log()" function in Section 1.11 as follows:

```
int log(int n){
    return n>1 ? log(n/2)+1 : 0;
} /* compute log(n) recursively */
```

The "factorial" function in Section 1.11 can also be implemented most elegantly using recursion. This implementation uses the definition of the factorial function:

n! = { 1 if n = 0, n(n-1)! if n > 0. }

This recursive (or inductive) definition is used in the following code:

```
int factorial(int n){
    return n>1 ? n * factorial(n-1) : 1;
} /* compute n! using recursion */
```

Again, this implementation may be slightly less efficient than the original one in Section 1.11 because of the extra memory allocations for the arguments and output in each recursive call. Still, it is particularly short and elegant, and it follows the spirit of the above mathematical definition.

Here is another example that has something to do with the factorial function. For any number a and a nonnegative integer number n, define

C(a,n) ≡ a(a-1)(a-2)⋯(a-(n-1)) = { 1 if n = 0, a C(a-1,n-1) if n ≥ 1. }

In particular, if a is a nonnegative integer number, then

C(a,n) = { a! / (a-n)! if a ≥ n, 0 if a < n. }

Here is the recursive implementation of this function:

```
int C(int a, int n){
    return n ? a * C(a-1,n-1) : 1;
} /* a!/(a-n)! */
```