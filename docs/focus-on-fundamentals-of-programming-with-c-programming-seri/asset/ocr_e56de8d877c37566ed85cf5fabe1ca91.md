# Note that the call:

```
swap(&x, &y);
```

transmits the addresses of the actual parameters x and y rather than their values. This means that the formal parameters u and v will have addresses as their values. Therefore, they should be declared as pointers with the function prototype:

```
void swap(int *u, int *v);
```