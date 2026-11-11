```
```
void fun(int &first, int &second)
```
```

If the call to fun happens to pass the same variable twice, as in

```
```
fun(total, total)
```
```

then first and second in fun will be aliases.

Second, collisions between array elements can also cause aliases. For example, suppose the function fun is called with two array elements that are specified with variable subscripts, as in

```
```
fun(list[i], list[j])
```
```

If these two parameters are passed by reference and i happens to be equal to j, then first and second are again aliases.

Third, if two of the formal parameters of a subprogram are an element of an array and the whole array, and both are passed by reference, then a call such as

```
```
fun1(list[i], list)
```
```

could result in aliasing in fun1, because fun1 can access all elements of list through the second parameter and access a single element through its first parameter.

Still another way to get aliasing with pass-by-reference parameters is through collisions between formal parameters and nonlocal variables that are visible. For example, consider the following C code:

```
```
int * global;
void main() {
    ...
    sub(global);
    ...
}
void sub(int * param) {
    ...
}
```
```

Inside sub, param and global are aliases.

All these possible aliasing situations are eliminated if pass-by-value-result is used instead of pass-by-reference. However, in place of aliasing, other problems sometimes arise, as discussed in Section 9.5.2.3.

# **9.5.2.5 Pass-by-Name**

Pass-by-name is an inout-mode parameter transmission method that does not correspond to a single implementation model. When parameters are passed by name, the actual parameter is, in effect, textually substituted for the corresponding