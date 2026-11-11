```
"India"
};
```

declares **name** to be an *array of three pointers* to characters, each pointer pointing to a particular name as:

name[0] ──> New Zealand  
name[1] ──> Australia  
name[2] ──> India

This declaration allocates only 28 bytes, sufficient to hold all the characters as shown

<table>
<tr><td>N</td><td>e</td><td>w</td><td>Z</td><td>e</td><td>a</td><td>l</td><td>a</td><td>n</td><td>d</td><td>\0</td></tr>
<tr><td>A</td><td>u</td><td>s</td><td>t</td><td>r</td><td>a</td><td>l</td><td>i</td><td>a</td><td>\0</td><td></td></tr>
<tr><td>I</td><td>n</td><td>d</td><td>i</td><td>a</td><td>\0</td><td></td><td></td><td></td><td></td><td></td></tr>
</table>

The following statement would print out all the three names:

```
for(i = 0; i <= 2; i++)
    printf("%s\n", name[i]);
```

To access the jth character in the ith name, we may write as

```
*(name[i]+j)
```

The character arrays with the rows of varying length are called 'ragged arrays' and are better handled by pointers.

Remember the difference between the notations `*p[3]` and `(*p)[3]`. Since `*` has a lower precedence than `[ ]`, `*p[3]` declares p as an array of 3 pointers while `(*p)[3]` declares p as a pointer to an array of three elements.

# ## 13.13 POINTERS AS FUNCTION ARGUMENTS

**LO 13.6**

We have seen earlier that when an array is passed to a function as an argument, only the address of the first element of the array is passed, but not the actual values of the array elements. If x is an array, when we call sort(x), the address of x[0] is passed to the function sort. The function uses this address for manipulating the array elements. Similarly, we can pass the address of a variable as an argument to a function in the normal fashion. We used this method when discussing functions that return multiple values (see Chapter 11).

When we pass addresses to a function, the parameters receiving the addresses should be pointers. The process of calling a function using pointers to pass the addresses of variables is known as 'call by reference'. (You know, the process of passing the actual value of variables is known as "call by value".) The function which is called by 'reference' can change the value of the variable used in the call.

Consider the following code:

```
main()
{
    int x;
    x = 20;
    change(&x);  /* call by reference or address */
    printf("%d\n",x);
```