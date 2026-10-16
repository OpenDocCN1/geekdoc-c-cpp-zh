A further complicating factor in C++ and C is that arrays are implicitly constant pointers to their first component. Thus, we can write code in C or C++ as follows:

```
int a[] = {1,2,3,4,5}; /* a[0] = 1, etc. */
int* p = a; /* p points to first component of a */
printf("%d\n", *p); /* prints value of a[0], so 1 */
printf("%d\n", *(p+2)); /* prints value of a[2]= 3 */
printf("%d\n", *(a+2)); /* also prints 3 */
printf("%d\n", 2[a]); /* also prints 3! */
```

Indeed, a[2] in C is just a shorthand notation for a + 2, and, by the commutativity of addition, we can equivalently write 2[a]!

Pointers are most useful in the creation of recursive types: a type that uses itself in its declaration. Recursive types are extremely important in data structures and algorithms, since they naturally correspond to recursive algorithms, and represent data whose size and structure is not known in advance, but may change as computation proceeds. Two typical examples are lists and binary trees. Consider the following C-like declaration of lists of characters:

```
struct CharList{
    char data;
    struct CharList next; /* not legal C! */
};
```

There is no reason in principle why such a recursive definition should be illegal; recursive functions have a similar structure. However, a close look at this declaration indicates a problem: Any such data must contain an infinite number of characters! In the analogy with recursive functions, this is like a recursive function without a “base case,” that is, a test to stop the recursion:

```
int factorial (int n){
    return n * factorial (n - 1);      /* oops */
}
```

This function lacks the test for small n and results in an infinite number of calls to factorial (at least until memory is exhausted). We could try to remove this problem in the definition of CharList by providing a base case using a union:

```
union CharList{
    enum { nothing } emptyCharList; /* no data */
    struct{
        char data;
        union CharList next; /* still illegal */
    } charListNode;
};
```