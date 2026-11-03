We know that rarely the individual strings will be of equal lengths. Therefore, instead of making each row a fixed number of characters, we can make it a pointer to a string of varying length. For example,

```
```c
static char *name[3] = {
  "New Zealand",
  "Australia",
  "India"
};
```
```

declares name to be an array of three pointers to characters, each pointer pointing to a particular name as shown below:

+   - name[0] → New Zealand
+   - name[1] → Australia
+   - name[2] → India

This declaration allocates only 28 bytes, sufficient to hold all the characters as shown below:

| N | e | w | Z | e | a | l | a | n | d | \0 |
|---|---|---|---|---|---|---|---|---|---|-----|
| A | u | s | t | r | a | l | i | a | \0 |  |
| I | n | d | i | a | \0 |  |  |  |  |  |

The following statement would print out all the three names:

```
```c
for(i = 0; i <= 2; i++)
  printf("%s\n", name[i]);
```
```

To access the jth character in the ith name, we may write as

```
```c
*(name[i]+j)
```
```

The character arrays with the rows of varying length are called ragged arrays and are better handled by pointers.

Remember the difference between the notations *p[3] and (*p)[3]. Since * has a lower precedence than [], *p[3] declares p as an array of 3 pointers while (*p)[3] declares p as a pointer to an array of three elements.

# 11.10 POINTERS AND FUNCTIONS

# Pointers as Function Arguments

We have noted earlier that when an array is passed to a function as an argument, only the address of the first element of the array is passed, but not the actual values of the array elements. If x is an array, when we call sort(x), the address of x[0] is passed to the function sort. The function uses this address for manipulating the array elements. Similarly, we can pass the address of a variable as an argument to a function in the normal fashion.

When we pass addresses to a function, the parameters receiving the addresses should be pointers. The process of calling a function using pointers to pass the addresses of variable is known as call by reference. (You know, the process of passing the actual value of variables is known as call by value.) The function which is called by 'reference' can change the value of the variable used in the call. Consider the following code: