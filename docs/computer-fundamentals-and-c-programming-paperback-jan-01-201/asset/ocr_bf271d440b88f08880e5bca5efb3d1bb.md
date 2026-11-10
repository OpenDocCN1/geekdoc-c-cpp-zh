The compiler is not confused by the inconsistency of form as long as the types match. However, it would be unwise to take advantage of this equivalence in this manner.

# 12.12.2  Using const to Protect an Array from a Function

Creating an array and initializing its elements involve overheads that can be significant for large arrays. C eliminates this overhead by copying the pointer and not the array, when the array name is used as an argument. In most cases, this property is in sync with our requirements because we usually access and update a single array. There’s no point in copying an array of a thousand elements if all we need is to simply search it. However, this saving also comes at a price: the array is no longer secure.

We pass the value of a variable or its address depending on whether we want to protect the original variable or have it changed by the function. An array doesn’t provide this option because by passing its name as argument, we make it *completely* accessible to the function. C has two solutions to this problem. The first one is known to you (5.13.2); use the **const** qualifier to declare the array:

```
const short arr[SIZE] = {10, 10, 10, 10, 10, 10};
```

This array can never be changed—either directly or by using a function. Arrays meant only for lookup should be declared in this way. But if the intention is to protect the array from modification *only* by a function, then use **const** in the function signatures in the following manner:

```
void print_array(const short arr[], short size);  *Array notation*\nvoid print_array(const short *arr, short size);  *Pointer notation*
```

**print_array** can’t now change the array pointed to by arr even though the array may be otherwise changeable. Many of our previous programs could be made safer using **const**. For instance, the **merge_arrays** function (Program 11.6) should be declared in the following manner to protect the array, a, from being written by the function:

```
void merge_arrays(const short a[], short m, const short b[], short n, short c[]);
```

You must now develop the habit of using the **const** keyword in function signatures wherever it is relevant. Chapter 13, which deals with string manipulation, uses this keyword extensively. Section 12.18 examines the three possible ways of using the **const** qualifier in the declaration of a pointer.

> **Tip:** If an array is not to be modified in any way, then declare it as constant using the **const** keyword. But if a specific function is to be prevented from changing the array, then use the **const** keyword in the function prototype and header of the definition.

![](bbox=[0.087, 0.733, 0.138, 0.771])

# 12.12.3  Returning a Pointer to an Array

A function can return a pointer to an array, but where should you create this array? If you create it inside the function, then the array can’t be declared in the regular manner (i.e., automatic) because the object would vanish after the function terminates. Program 12.10 offers a simple solution by creating a **static** array in the function body. This array is also visible in **main** because the function returns a pointer to it. Observe the * preceding the function name; **days_in_month** returns a pointer to short.