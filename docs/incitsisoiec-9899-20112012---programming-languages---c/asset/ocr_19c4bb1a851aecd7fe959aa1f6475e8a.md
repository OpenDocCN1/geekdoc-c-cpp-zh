structures: w[0].a[0] is 1 and w[1].a[0] is 2; all the other elements are zero.

# 29 EXAMPLE 6 The declaration

```
short q[4][3][2] = {
 { 1 },
  { 2, 3 },
  { 4, 5, 6 }
};
```

contains an incomplete but consistently bracketed initialization. It defines a three-dimensional array object q[0][0][0] is 1, q[1][0][0] is 2, q[1][0][1] is 3, and 4, 5, and 6 initialize q[2][0][0]. q[2][0][1] is 1, and q[2][1][0] respectively: all the rest are zero. The initializer for q[0][0][0] does not begin with a left brace, so up to six items from the current list may be used. There is only one, so the values for the five elements are initialized with zero. Likewise, the initializers for q[1][0] and q[2][0] do not begin with a left brace, so each uses up to six items, initializing their respective two-dimensional subaggregates. If there had more than six items in any of the lists, a diagnostic message would have been issued.

```
short q[4][3][2] = {
 1, 0, 0, 0, 0,
  2, 3, 0, 0, 0,
  4, 5, 6
}
```

or by:

```
short q[4][3][2] = {
 { 1 },
 {
 { 2, 3 },
 {
 { 4, 5 },
 { 6 },
 };};
```

in a fully bracketed format.

30 Note that the fully bracketed and minimally bracketed forms of initialization are, in general, less likely to cause confusion.

# 31 EXAMPLE 7 One form of initialization that completes array types involves typedefed names. Given the declaration

```
typedef int a[]; // OK - declared with block scope
```

the declaration

```
A a = { 1, 2 }, b = { 3, 4, 5 };
```

is identical to

```
int a[] = { 1, 2 }, b[] = { 3, 4, 5 };
```

due to the rules for incomplete types.