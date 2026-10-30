function. In addition, the calling program might also have to deal with post-conditions, as will be discussed in Section 9.4.

+   2. Responsibilities of the called program: If the calling program fullfills its responsibilities (i.e. the arguments satisfy the preconditions), and only if the calling program fullfills its responsibilities, is the called program obliged to do whatever was promised. There is no telling what will happen if the preconditions are not satisfied. Thus in case of gcd, if a negative value or zero is supplied: nonsense values may be returned, or the program may never terminate, or terminate with an error.

It is extremely important to clearly write down the specification of a function. You may sometimes avoid doing so, thinking that the specification is obvious. But it may not be so! For example, a more general definition of GCD might allow one of the numbers to be zero, in which case the other number is defined to be the GCD. If this is the definition a user is familiar with, he/she might supply 0 as the value of the second parameter n. This will certainly cause the program to terminate because of a division by zero in the very first step of our code. To prevent such misunderstandings, it is best to write down the specifications in full detail.

The natural place to write down the specification is immediately before the function definition. So your function for gcd should really look like the following.

```
int gcd(int L, int S)
// Function for computing the greatest common divisor of integers L, S.
// PRE-CONDITION: L, S > 0
{
...
}
```

Please get into the habit of writing specifications for all the functions that you write. Note that in the specification it is important to not write how the function does what it does, but only what the function does, and for what preconditions.

A description of how the function does what it does, often referred to as the description of the implementation of the function is also important. But this should be kept separate from the specification. The description of how can be in a separate document, or could be written as comments in the body of the code of the function. For example, the following comment might be useful to explain how the gcd function works.

```
// Note the theorem: If n divides m, then GCD(m,n) = n.
//                 If n does not divide m, then GCD(m,n) = GCD(n, m mod n)
```

This comment could be placed at the beginning of the loop.

# 9.4 Functions that do not return values

Every function (or command) does not need to return a value. You have already seen such functions, e.g. forward, which causes the turtle to move forward, but itself does not stand