
# Chapter 12 691

## Passing Addresses

In contrast to passing addresses with references, addresses can be explicitly passed with pointers. To explicitly pass an address to a function, all you need to place the address operator, & in front of the variable being passed. For example, this function call `swap(&firstnum, &secnum);` passes the addresses of the variables `firstnum` and `secnum` to `swap()`, as shown in Figure 12.17. Explicitly passing addresses with the address operator is also referred to as a pass by reference because the called function can reference, or access, variables in the function by using the passed addresses. As you see in Section 6.3, references can also be made with references. In this section, you use the addresses passed with pointers to directly access the variables `firstnum` and `secnum` from `swap()` and exchange their values—procedure accomplished in Program 6.8 with reference parameters.

Variable name: firstnum
Variable address: an address

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_710_0.png)

Figure 12.17 Explicitly passing addresses to swap()

One of the first requirements in writing `swap()` is to construct a function header that receives and stores the passed values, in which case are two addresses. As you see in Section 12.1, addresses are stored in pointers, which means the parameters of `swap()` must be declared as pointers.

Assuming `firstnum` and `secnum` are double-precision variables and `swap()` returns no value, a suitable function header for `swap()` is as follows:

```
void swap(double *nm1Addr, double *nm2Addr);
```

The choice of the parameter names `nm1Addr` and `nm2Addr` is, with all parameters, up to the programmer. The declaration `double *nm1Addr`, however, states that the parameter named `nm1Addr` is used to store the address of a double-precision value. Similarly, the declaration `double *nm2Addr` specifies that `nm2Addr` also stores the address of a double-precision value.

Before the body of `swap()` to exchange the values in `firstnum` and `secnum`, first check that the values accessed by using the addresses in `nm1Addr` and `nm2Addr` are correct. Program 12.10 performs this check.

The output displayed when Program 12.10 runs as follows:

The number whose address is in nm1Addr is 20.5
The number whose address is in nm2Addr is 6.25

# 692 Pointers

## Program 12.10

```
#include <iostream>
using namespace std;

void swap(double *, double *); // function prototype

int main()
{
    double firstnum = 20.5, secnum = 6.25;

    swap(&firstnum, &secnum); // call swap

    return 0;
}

// this function illustrates passing pointer arguments
void swap(double *nm1Addr, double *nm2Addr)
{
    cout << "The number whose address is in nm1Addr "
         << nm1Addr << endl;
    cout << "The number whose address is in nm2Addr "
         << nm2Addr << endl;

    return;
}
```

The declaration declares that `swap()` returns value directly, and its parameters are two pointers that "point to" double-precision values. When the function is called, it requires two pointers to be passed, and each address is the address of a double-precision value.

Second, the indirection operator is used in `swap()` to access the values stored in `firstnum` and `secnum`. The `swap()` function has no knowledge of these variable names, but it does the address of `firstnum` in `nm1Addr` and the address of `secnum` in `nm2Addr`. The expression `*nm1Addr` means "the variable whose address is in nm1Addr." It is, of course, the variable `firstnum`. Similarly, the second statement obtains the value stored in `secnum` as "the variable whose address is in nm2Addr." Pointers have been used successfully to allow `swap()` to access variables in `main()`. Figure 12.18 illustrates storing addresses in parameters.

# Chapter 12 693

Passing Addresses

Parameter name: nm1Addr `swap(&firstnum, &secnum)`
Parameter name: nm2Addr `&secnum`

Figure 12.18 Storing addresses in parameters

Having verified that `swap()` can access `main()`'s `firstnum` and `secnum`, you can now expand `swap()` to exchange the values in these variables. The values in `main()`'s variables `firstnum` and `secnum` can be interchanged within `swap()` using the three-step algorithm described in Section 6.3:
1. firstnum's value in a temporary location.
2. secnum's value in firstnum.
3. The temporary location's value in secnum.

Using pointers in `swap()`, this algorithm takes the following form:
1. Store the value of the variable that `nm1Addr` points to in a temporary location by the statement `temp = *nm1Addr` (see Figure 12.19).

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_712_0.png)

Figure Indirectly storing firstnum's value
2. Store the value of the variable whose address is in `nm2Addr` in `nm1Addr` using the statement `*nm1Addr = *nm2Addr` (see Figure 12.20).
3. Move the value in the temporary location into the variable whose address is in `nm2Addr` using the statement `*nm2Addr = temp;` (see Figure 12.21).

# 694 Pointers

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_713_0.png)

Figure 12.20 Indirect changing firstnum's value
![](img/e2a849fc7bc04aa2e6669ad865e0c22b_713_1.png)

Figure 12.21 Indirect changing secnum's value

Program 12.11 contains the final form of `swap()`, written according to this description.

## Program 12.11

```
#include <iostream>
using namespace std;

void swap(double *, double *); // function prototype

int main() {
    double firstnum = 20.5, secnum = 6.25;
    cout << "The value stored in firstnum: " << firstnum << endl;
    cout << "The value stored in secnum: " << secnum << "\n";
}
```

```
cout << "The value stored in firstnum: " << firstnum << endl;
cout << "The value stored in secnum: " << secnum << "\n";
```

# Chapter 12 695

Passing Addresses

```
swap(&firstnum, &secnum); // call swap
cout << "The value stored in firstnum is now: " << firstnum << endl;
cout << "The value stored in secnum is now: " << secnum << endl;

return 0;

// this function swaps the values in its two arguments
void swap(double *nm1Addr, double *nm2Addr)
{
    double temp;

    temp = *nm1Addr; // save firstnum's value
    *nm1Addr = *nm2Addr; // move secnum's value into firstnum
    *nm2Addr = temp; // change secnum's value

    return;
}
```

A sample run of Program 12.11 produced this output:

The value stored in firstnum: 20.5
The value stored in secnum: 6.25

The value stored in firstnum: 6.25
The value stored in secnum: 20.5

As this output shows, the values stored in `main()` variables have been modified in `swap()`, which was made possible using pointers. To make sure you understand, compare this version of `swap()` with the version using references in Program 6.10. The advantage of using pointers rather than references is that the function specifies that addresses are being used, which is an alert that will likely affect other variables of the calling function. The advantage of using references is that the notation is much simpler. Generally, for functions such as `swap()`, case of notation winds out, and references are used. In passing arrays to functions, however, which is the next topic, the compiler passes an address automatically, which dictates using pointers to store the address.

## Passing Arrays

When an array is passed to a function, its address is the only item actually passed. "Address" means the address of the first location used to store the array, as shown in Figure 12.22. Because the first location reserved for an array corresponds to element 0 of the array, the "address of the array" is also the address of element 0.

# 696 Pointers

An array is a series of memory locations

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_715_0.png)

Figure 12.22 An array's address is the address of the first location reserved for the array

For a specific example of passing an array to a function, examine Program 12.12. In this program, the `nums` array is passed to the `findMax()` function, using conventional notation.

## Program 12.12

```
#include <iostream>
using namespace std;

int findMax(int vals[], int); // function prototype

int main() {
    const int NUMPTS = 5;
    int nums[NUMPTS] = {2, 18, 1, 27, 16};

    cout << "\nThe maximum value is "
         << findMax(nums, NUMPTS) << endl;
    return 0;
}

// this function returns the maximum value in an array of ints
int findMax(int vals[], int numels) {
    int i, max = vals[0];

    for (i = 1; i < numels; i++)
        if (max < vals[i])
            max = vals[i];

    return max;
}
```

The following output is displayed when Program 12.12 runs:

The maximum value is 27
