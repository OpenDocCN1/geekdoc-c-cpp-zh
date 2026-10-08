# 414 One-Dimensional Arrays

```
c. int i, a[5] = {2, 5, 6, 7, 12};
int b[5] = {5, 3, 6, 1, 2};

for(i = 0; i < 5; i++) {
  a[i] = a[i] + b[3];
  b[i] = a[i] * b[2];\}
```

![](bbox=[0.665, 0.115, 0.885, 0.245])

Given the following arrays show the results of the following arithmetic operations.

```
a[5] = { 6, 9, 5, 4, 25};
float b[5] = {12.5, 6.4, 3.4, 2.6, 1.5};
```

```
a[i] = a[i] / 4; i = 0 ...4
b[i] = b[i] / 2; i = 0 ...4
a[i] = a[i] + b[i]; i = 0 ...4
a[i] = a[i] - b[i]; i = 0 ...4
```

# 7.5 Passing Arrays to Functions

Arrays may be passed to functions. An array may be passed to a function as a whole or element-by-element. The following sections show both ways of passing an array.

# 7.5.1 Passing Fixed-Size Arrays

The following code shows how to pass an entire array to a function:

```
void func1(int [], float [], int);    /* function prototype */
int main() {
  int a[5], arsize = 5;
  float b[5];
  ...
  func1(a, b, arsize);                /* function call */
```