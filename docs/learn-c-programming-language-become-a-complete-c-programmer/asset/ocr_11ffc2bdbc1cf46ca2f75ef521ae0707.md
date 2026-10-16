The dimensions **3** and **5** exist in the compiler source only. When we write code, it is our job to remember them somehow and supply the dimensions where needed. For example, we might print `ma` like this:

```
void print_ma()
{
for (int i = 0; i!=3; i++) {
for (int j = 0; j!=5; j++)
cout << ma[i][j] << '\t';
cout << '\n';
}
}
```

The comma notation used for array bounds in some languages cannot be used in C++ because the comma (,) is a sequencing operator (§10.3.2). Fortunately, most mistakes are caught by the compiler. For example:

```
int bad[3,5];
int good[3][5];
int ouch = good[1,4]; int nice = good[1][4];

// error : comma not allowed in constant expression
// 3 arrays with 5 ints each
// error : int initialized by int* (good[1,4] means good[4], which is an int*)
```

# 7.4.3 Passing Arrays

Arrays cannot directly be passed by value. Instead, an array is passed as a pointer to its first element. For example:

```
void comp(double arg[10]) // arg is a double*
{
for (int i=0; i!=10; ++i) arg[i] +=99;
}

void f() {
double a1[10]; double a2[5]; double a3[100];

comp(a1);
comp(a2); // disaster!
comp(a3); // uses only the first 10 elements
};
```

This code looks sane, but it is not. The code compiles, but the call `comp(a2)` will write beyond the bounds of `a2`. Also, anyone who guessed that the array was passed by value will be disappointed: the writes to `arg[i]` are writes directly to the elements of `comp()`’s argument, rather than to a copy. The function could equivalently have been written as

```
void comp(double* arg)
{
```