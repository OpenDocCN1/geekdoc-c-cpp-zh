The output of Listing 11.12 (cleararray.cpp) is

```
2 4 6 8
0 0 0 0
```

The clear function actually modifies the contents of main's list array. The function works on the array's actual elements, not copies of its elements.

Arrays, therefore, by default are passed by reference with respect to the elements they contain. By default, an array's contents are open to corruption by errant functions. In order to protect an array so that a function may read its contents but not modify its contents, the parameter must be declared const, as in

```
int sum(const int a[], int n)
```

In Listing 11.11 (arrayofunc.cpp) there is no reason why the print and sum functions should be able to modify the contents of their array parameters, so the const specifier should be added to their definitions.

As a general rule, all functions that accept array parameters should declare the array contents as const unless they need to modify the elements of the array.

> As a general rule, all functions that accept array parameters should declare the array contents as const unless they need to modify the elements of the array. For example, use
> `int sum(const int a[], int n)`
> rather than
> `int sum(int a[], int n)`
> if the sum function must be able to examine the contents of the array but is not intended to modify its contents.

C++ does not directly support empty arrays. A physical array must contain at least one element. Sometimes it is appropriate to consider an array that is conceptually empty: for example, what if we wish to pass an "empty" array to the sum function? We can pass 0 as the second parameter since empty array contains no elements, but what should we pass as the first parameter? Any array will do, but there is no need create a real array when none truly is needed. Instead, we may use nullptr:

```
quantity = sum(nullptr, 0);
```

If you scrutinize the body of the sum function, you will see that this call will assign to quantity the correct answer, namely zero.

# 11.2.2 Pointers and Arrays

An array name used in C++ source code references a location in memory, the address of the first element (element at index 0) in the array. In this way an array name is similar to a constant pointer (see Section 10.7 for more information about C++ pointers). Because of this, we can treat in some ways an array identifier like a pointer. Similarly, we can direct a pointer to point to an array, and then treat the pointer itself as if it were an array.

Listing 11.13 (pointerprint.cpp) uses a pointer to traverse an array.