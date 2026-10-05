# 200 Introduction to C++

Therefore, in the general case we have:

+   * a[i]+j is equivalent to &a[i][j].
* *(a[i]+j) is equivalent to a[i][j].

And because as we know now, a[i] is converted to *(a+i) when we have:

+   * *(a+i)+j is equivalent to &a[i][j].
* **(a+i)+j) is equivalent to a[i][j].

An example of these equations is that a[0][0] is equivalent to *a[0] and **a. Essentially, when we write a[i][j] the compiler converts it to *(a+i)+j). To sum up, the following program uses three ways to display the elements of a two-dimensional array.

Needless to say which one is the simplest...
Let's add this. Consider the following declarations:

```
int a[2][3], b[10];
```

My question is: As we saw that b can be used as a pointer to b[0], is it correct to say that a can be used as a pointer to a[0][0]?nC++ treats a as a one-dimensional array, the answer is no, can a be used as a pointer to the first element, that is, a[0]. Therefore, if we want to assign a to a pointer variable, what will be the type of the pointer? It should be pointer to an array. For example:

```
int (*p)[3]; /* The parentheses are necessary, otherwise the compiler would interpret p as an array of three pointers to integers. */
np = a;
```

and p points to the first element of such row of a, that is, a[0][0].

> Remember, in a declaration such as int x[5], "x" "decays" to a pointer, while in a declaration such as int y[5][3], y does not "decay" to a pointer, but to a pointer to array.

A note of that: the type of the expression &x is a pointer to an array of five integers, while the type of the expression &y is a pointer to an array of five arrays where each array contains three integers.