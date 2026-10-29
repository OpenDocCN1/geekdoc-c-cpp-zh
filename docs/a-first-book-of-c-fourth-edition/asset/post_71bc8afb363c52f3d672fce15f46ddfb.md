
## Arrays and Pointers

The following output is displayed when Program 8.13 runs:

```
The maximum value is 27
```

The parameter named `vals` in the function header declaration for `findMax()` actually receives the address of the `nums` array. Therefore, `vals` is really a pointer because pointers are variables (or parameters) used to store addresses. Because the address passed to `findMax()` is the address of an integer, the following function header for `findMax()` is also suitable:

```
int findMax(int *vals, int nums)   // vals is declared as
                                  // a pointer to an integer
```

The declaration `int *vals` in the function header declares that `vals` is used to store an address of an integer. The address stored is, of course, the location of the beginning of an array. The following is a rewritten version of the `findMax()` function that uses the new pointer declaration for `vals` but retains the use of subscripts to refer to array elements:

```
int findMax(int *vals, int nums)   // find the maximum value
{
    int i, max = vals[0];

    for (i = 1; i < nums; i++)
        if (max < vals[i])
            max = vals[i];
    return max;
}
```

Regardless of how `vals` is declared in the function header or how it’s used in the function body, it’s truly a pointer variable. Therefore, the address in `vals` can be modified. This isn’t true for the name `nums`, however. Because `nums` is the name of the originally created array, it’s a pointer constant. As described in Section 8.2, this means the address in `nums` can’t be changed, and the address of `nums` can’t be taken. No such restrictions, however, apply to the pointer variable `vals`. Therefore, all the pointer arithmetic you learned in Section 8.3 can be applied to `vals`.

Following are two more versions of `findMax()`, both using pointers instead of subscripts. In the first version, you simply substitute pointer notation for subscript notation. In the second version, you use pointer arithmetic to change the address in the pointer. As stated, access to an array element with the subscript notation `arrayName[i]` can always be replaced by the pointer notation `*(arrayName + i)`.

In the first modification to `findMax()`, you make use of this correspondence by simply replacing all references to `vals[i]` with the expression `*(vals + i)`:

```
int findMax(int *vals, int numels)  // find the maximum value
{
    int i, max = *vals;
    for (i = 1; i < numels; i++)
        if (max < *(vals + i) )
            max = *(vals + i);
    return max;
}
```

The second modification of `findMax()` makes use of being able to change the address stored in `vals`. After each array element is retrieved by using the address in `vals`, the address is incremented by 1 in the altering list of the `for` statement. The expression `max = *vals` previously used to set `max` to the value of `vals[0]` is replaced by the expression `max = *vals++`, which adjusts the address in `vals` to point to the second array element. The element this expression assigns to `max` is the array element `vals` points to before it’s incremented. The postfix increment, `++`, doesn’t change the address in `vals` until after the address has been used to retrieve the first array element.

```
int findMax(int *vals, int numels)  // find the maximum value
{
    int i, max = *vals++;  // get the first element and increment it
    for (i = 1; i < numels; i++, vals++)
    {
        if (max < *vals)
            max = *vals;
    }
    return max;
}
```

Review this version of `findMax()`. Initially, the maximum value is set to "the thing pointed to by `vals`." Because `vals` initially contains the address of the first array element passed to `findMax()`, the value of this first element is stored in `max`. The address in `vals` is then incremented by 1. The 1 added to `vals` is scaled automatically by the number of bytes used to store integers. Therefore, after the increment, the address stored in `vals` is the address of the next array element, as shown in Figure 8.25. The value of this next element is compared with the maximum, and the address is again incremented, this time in the altering list of the `for` statement. This process continues until all array elements have been examined.

![](img/202cface8244f523c2641baa2e00d7dd_397_0.png)

**Figure 8.25 Pointing to different elements**

The version of `findMax()` you choose is a matter of personal style. Generally, beginning programmers feel more at ease using subscripts rather than pointers. Also, if the program uses an array as the natural storage structure for the application and data, an array access using subscripts is more appropriate to indicate the program’s intent clearly. However, as you learn more about data structures, pointers become an increasingly useful and powerful tool. In more complex data structures, there’s no simple or easy equivalence for subscripts.

There’s one more neat trick you can glean from this discussion. Because passing an array to a function actually involves passing an address, you can pass any valid address. For example, the function call `findMax(&nums[2], 3)` passes the address of `nums[2]` to `findMax()`. In `findMax()`, the pointer `vals` stores the address, and the function starts the search for a maximum at the element corresponding to this address. Therefore, from `findMax()`’s perspective, it has received an address and proceeds appropriately.

### Advanced Pointer Notation¹⁰

You can also access multidimensional arrays by using pointer notation, although the notation becomes more cryptic as the array dimensions increase. Pointer notation is especially useful with two-dimensional character arrays, and this section discusses pointer notation for two-dimensional numeric arrays. For example, examine this declaration:

```
int nums[2][3] = { {16,18,20}, {25,26,27} };
```

This declaration creates an array of elements and a set of pointer constants named `nums`, `nums[0]`, and `nums[1]`. Figure 8.26 shows the relationship between these pointer constants and the elements of the `nums` array.

![](img/202cface8244f523c2641baa2e00d7dd_398_0.png)

The availability of the pointer constants associated with a two-dimensional array enables you to access array elements in a variety of ways. One way is to view a two-dimensional array as an array of rows, with each row as an array of three elements. From this viewpoint, the address of the first element in the first row is provided by `nums[0]`, and the address of the first element in the second row is provided by `nums[1]`. Therefore, the variable pointed to by `nums[0]` is `nums[0][0]`, and the variable pointed to by `nums[1]` is `nums[1][0]`. Each element in the array can be accessed by applying an offset to the correct pointer. Therefore, the following notations are equivalent:

| Pointer Notation | Subscript Notation | Value |
| --- | --- | --- |
| `*nums[0]` | `nums[0][0]` | 16 |
| `*(nums[0] + 1)` | `nums[0][1]` | 18 |
| `*(nums[0] + 2)` | `nums[0][2]` | 20 |
| `*nums[1]` | `nums[1][0]` | 25 |
| `*(nums[1] + 1)` | `nums[1][1]` | 26 |
| `*(nums[1] + 2)` | `nums[1][2]` | 27 |

You can now go further and replace `nums[0]` and `nums[1]` with their pointer notations, using the address of `nums`. As shown in Figure 8.26, the variable pointed to by `nums` is `nums[0]`. That is, `*nums` is `nums[0]`. Similarly, `*(nums + 1)` is `nums[1]`. Using these relationships leads to the following equivalence:

| Pointer Notation | Subscript Notation | Value |
| --- | --- | --- |
| `*(*nums)` | `nums[0][0]` | 16 |
| `*(*nums + 1)` | `nums[0][1]` | 18 |
| `*(*nums + 2)` | `nums[0][2]` | 20 |
| `*(*(nums + 1))` | `nums[1][0]` | 25 |
| `*(*(nums + 1) + 1)` | `nums[1][1]` | 26 |
| `*(*(nums + 1) + 2)` | `nums[1][2]` | 27 |

The same notation applies when a two-dimensional array is passed to a function. For example, the two-dimensional array `nums` is passed to the `calc()` function by using the call `calc(nums);` As with all array passes, an address is passed. A suitable function header for the `calc()` function is as follows:

```
void calc(int pt[2][3])
```

As you have seen, the parameter declaration for `pt` can also be the following:

```
void calc(int pt[][3])
```

Using pointer notation, the following is another suitable declaration:

```
void calc(int (*pt)[3])
```

In this declaration, the inner parentheses are required to create a single pointer to arrays of three integers. Each array is, of course, equivalent to a single row of the `nums` array. By offsetting the pointer, each element in the array can be accessed. Notice that without the parentheses, the declaration becomes:

```
int *pt[3]
```

which creates an array of three pointers, each one pointing to a single integer. After the correct declaration for `pt` is made (any of the three valid declarations can be used), all the following notations in the `calc()` function are equivalent:

| Pointer Notation | Subscript Notation | Value |
| --- | --- | --- |
| `*(*pt)` | `pt[0][0]` | 16 |
| `*(*pt+1)` | `pt[0][1]` | 18 |
| `*(*pt+2)` | `pt[0][2]` | 20 |
| `*(*(pt+1))` | `pt[1][0]` | 25 |
| `*(*(pt+1)+1)` | `pt[1][1]` | 26 |
| `*(*(pt+1)+2)` | `pt[1][2]` | 27 |

The last two notions using pointers are seen in more advanced C++ programs. The first occurs because functions can return any valid C++ scalar data type, including pointers to any of these data types. If a function returns a pointer, the data type being pointed to must be declared in the function’s declaration. For example, the declaration

```
int *calc()
```

declares that `calc()` returns a pointer to an integer value, which means the address of an integer variable is returned. Similarly, the declaration

```
double *taxes()
```

declares that `taxes()` returns a pointer to a double-precision value, which means the address of a double-precision variable is returned.

In addition to declaring pointers to integers, double-precision numbers, and C++’s other data types, you can declare pointers that point to (contain the address of) a function. Pointers
