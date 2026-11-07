
```cpp
    break;
}
else if (temp < 0)       // signal to terminate
    break;
ar[i] = temp;
}
return i;
}

// the following function can use, but not alter,
// the array whose address is ar
void show_array(const double ar[], int n)
{
    using namespace std;
    for (int i = 0; i < n; i++)
    {
        cout << "Property #" << (i + 1) << ": $";
        cout << ar[i] << endl;
    }
}

// multiplies each element of ar[] by r
void revalue(double r, double ar[], int n)
{
    for (int i = 0; i < n; i++)
        ar[i] *= r;
}
```

Here are two sample runs of the program in Listing 7.7:

```text
Enter value #1: 100000
Enter value #2: 80000
Enter value #3: 222000
Enter value #4: 240000
Enter value #5: 118000
Property #1: $100000
Property #2: $80000
Property #3: $222000
Property #4: $240000
Property #5: $118000
Enter revaluation factor: 0.8
Property #1: $80000
Property #2: $64000
Property #3: $177600
Property #4: $192000
Property #5: $94400
Done.
```

```text
Enter value #1: 200000
Enter value #2: 84000
Enter value #3: 160000
Enter value #4: -2
Property #1: $200000
Property #2: $84000
Property #3: $160000
Enter revaluation factor: 1.20
Property #1: $240000
Property #2: $100800
Property #3: $192000
Done.
```

Recall that `fill_array()` prescribes that input should quit when the user enters five properties or enters a negative number, whichever comes first. The first output example illustrates reaching the five-property limit, and the second output example illustrates that entering a negative value terminates the input phase.

### Program Notes

We've already discussed the important programming details related to the real estate example, so let's reflect on the process. You began by thinking about the data type and designed appropriate functions to handle the data. Then you assembled these functions into a program. This is sometimes called *bottom-up programming* because the design process moves from the component parts to the whole. This approach is well suited to OOP, which concentrates on data representation and manipulation first. Traditional procedural programming, on the other hand, leans toward *top-down programming*, in which you develop a modular grand design first and then turn your attention to the details. Both methods are useful, and both lead to modular programs.

### The Usual Array Function Idiom

Suppose you want a function to process an array, say, of type `double` values. If the function is intended to modify the array, the prototype might look like this:

```cpp
void f_modify(double ar[], int n);
```

If the function preserves values, the prototype might look like this:

```cpp
void f_no_change(const double ar[], int n);
```

Of course, you can omit the variable names in the prototypes, and the return type might be something other than `void`. The main points are that `ar` really is a pointer to the first element of the passed array and that because the number of elements is passed as an argument, either function can be used with any size of array as long as it is an array of `double`:

```cpp
double rewards[1000];
double faults[50];
. . .
f_modify(rewards, 1000);
f_modify(faults, 50);
```

This idiom (pass the array name and size as arguments) works by passing two numbers—the array address and the number of elements. As you have seen, the function loses some knowledge about the original array; for example, it can’t use `sizeof` to get the size and relies on you to pass the correct number of elements.

### Functions Using Array Ranges

As you’ve seen, C++ functions that process arrays need to be informed about the kind of data in the array, the location of the beginning of the array, and the number of elements in the array. The traditional C/C++ approach to functions that process arrays is to pass a pointer to the start of the array as one argument and to pass the size of the array as a second argument. (The pointer tells the function both where to find the array and the kind of data in it.) That gives the function the information it needs to find all the data.

There is another approach to giving a function the information it needs: specify a range of elements. This can be done by passing two pointers—one identifying the start of the array and one identifying the end of the array. The C++ Standard Template Library (STL; presented in Chapter 16, “The string Class and the Standard Template Library”), for example, generalizes the range approach. The STL approach uses the concept of “one past the end” to indicate an extent. That is, in the case of an array, the argument identifying the end of the array would be a pointer to the location just after the last element. For example, suppose you have this declaration:

```cpp
double elboud[20];
```

Then the two pointers `elboud` and `elboud + 20` define the range. First, `elboud`, being the name of the array, points to the first element. The expression `elboud + 19` points to the last element (that is, `elboud[19]`), so `elboud + 20` points to one past the end of the array. Passing a range to a function tells it which elements to process. Listing 7.8 modifies Listing 7.6 to use two pointers to specify a range.

Listing 7.8  **arrfun4.cpp**

```cpp
// arrfun4.cpp -- functions with an array range
#include <iostream>
const int ArSize = 8;
int sum_arr(const int * begin, const int * end);
int main()
{
    using namespace std;
    int cookies[ArSize] = {1,2,4,8,16,32,64,128};
    // some systems require preceding int with static to
    // enable array initialization

    int sum = sum_arr(cookies, cookies + ArSize);
    cout << "Total cookies eaten: " << sum << endl;
    sum = sum_arr(cookies, cookies + 3);     // first 3 elements
    cout << "First three eaters ate " << sum << " cookies.\n";
    sum = sum_arr(cookies + 4, cookies + 8);    // last 4 elements
    cout << "Last four eaters ate " << sum << " cookies.\n";
    return 0;
}

// return the sum of an integer array
int sum_arr(const int * begin, const int * end)
{
    const int * pt;
    int total = 0;

    for (pt = begin; pt != end; pt++)
        total = total + *pt;
    return total;
}
```

Here’s the output of the program in Listing 7.8:

```text
Total cookies eaten: 255
First three eaters ate 7 cookies.
Last four eaters ate 240 cookies.
```

### Program Notes

In Listing 7.8, notice the for loop in the `sum_arr()` function:

```cpp
for (pt = begin; pt != end; pt++)
    total = total + *pt;
```

It sets pt to point to the first element to be processed (the one pointed to by begin) and adds *pt (the value of the element) to total. Then the loop updates pt by incrementing it, causing it to point to the next element. The process continues as long as pt != end. When pt finally equals end, it’s pointing to the location following the last element of the range, so the loop halts.

Second, notice how the different function calls specify different ranges within the array:

```cpp
int sum = sum_arr(cookies, cookies + ArSize);
...
sum = sum_arr(cookies, cookies + 3);       // first 3 elements
...
sum = sum_arr(cookies + 4, cookies + 8);   // last 4 elements
```

The pointer value cookies + ArSize points to the location following the last element. (The array has ArSize elements, so cookies[ArSize - 1] is the last element, and its address is cookies + ArSize - 1.) So the range cookies, cookies + ArSize specifies the entire array. Similarly, cookies, cookies + 3 specifies the first three elements, and so on.

Note, by the way, that the rules for pointer subtraction imply that, in `sum_arr()`, the expression `end - begin` is an integer value equal to the number of elements in the range. Also note that it’s important to pass the pointers in the correct order; the code assumes that `end` comes after `begin`.

### Pointers and const

Using const with pointers has some subtle aspects (pointers always seem to have subtle aspects), so let’s take a closer look. You can use the const keyword two different ways with pointers. The first way is to make a pointer point to a constant object, and that prevents you from using the pointer to change the pointed-to value. The second way is to make the pointer itself constant, and that prevents you from changing where the pointer points. Now for the details.

First, let’s declare a pointer `pt` that points to a constant:

```cpp
int age = 39;
const int * pt = &age;
```

This declaration states that `pt` points to a `const int` (39, in this case). Therefore, you can’t use `pt` to change that value. In other words, the value `*pt` is const and cannot be modified:

```cpp
*pt += 1;       // INVALID because pt points to a const int
cin >> *pt;     // INVALID for the same reason
```

Now for a subtle point. This declaration for `pt` doesn’t necessarily mean that the value it points to is really a constant; it just means the value is a constant insofar as `pt` is concerned. For example, `pt` points to `age`, and `age` is not const. You can change the value of `age` directly by using the `age` variable, but you can’t change the value indirectly via the `pt` pointer:

```cpp
*pt = 20;       // INVALID because pt points to a const int
age = 20;       // VALID because age is not declared to be const
```

Previous examples have assigned the address of a regular variable to a regular pointer. This example assigns the address of a regular variable to a pointer-to-const. That leaves two other possibilities: assigning the address of a const variable to a pointer-to-const and assigning the address of a const to a regular pointer. Are they both possible? The first is, and the second isn’t:

```cpp
const float g_earth = 9.80;
const float * pe = &g_earth;   // VALID
```

```cpp
const float g_moon = 1.63;
float * pm = &g_moon;          // INVALID
```

For the first case, you can use neither `g_earth` nor `pe` to change the value 9.80. C++ doesn’t allow the second case for a simple reason: If you can assign the address of `g_moon` to `pm`, then you can cheat and use `pm` to alter the value of `g_moon`. That makes a mockery
