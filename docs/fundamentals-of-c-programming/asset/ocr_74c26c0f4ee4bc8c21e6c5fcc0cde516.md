```
10
9
8
7
6
5
4
3
2
1
0
```

but the invocation

```
countdown(5)
```

displays

```
5
4
3
2
1
0
```

As we can see, when the caller does not supply a parameter specified by a function, and that parameter has a default value, the default value is used during the caller's call.

We may mix non-default and default parameters in the parameter lists of a function declaration, but all default parameters within the parameter list must appear after all the non-default parameters. This means the following definitions are acceptable:

```
int sum_range(int n, int m=100) { // OK, default follows non-default
    int sum = 0;
    for (int val = n; val <= m; val++)
        sum += val;
    return val;
}
```

and

```
int sum_range(int n=0, int m=100) { // OK, both default
    int sum = 0;
    for (int val = n; val <= m; val++)
        sum += val;
    return val;
}
```

but the following definition is illegal, since a default parameter precedes a non-default parameter in the function's parameter list:

```
int sum_range(int n=0, int m) { // Illegal, non-default follows default
    int sum = 0;
    for (int val = n; val <= m; val++)
```