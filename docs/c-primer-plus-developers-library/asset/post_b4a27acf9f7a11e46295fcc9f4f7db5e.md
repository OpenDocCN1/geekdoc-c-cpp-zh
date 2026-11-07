
```cpp
countdown(n-1);    // function calls itself
cout << n << ": Kaboom!\n";
}
```

Here’s the annotated output of the program in Listing 7.16:

```text
Counting down ... 4    <level 1; adding levels of recursion>
Counting down ... 3    <level 2>
Counting down ... 2    <level 3>
Counting down ... 1    <level 4>
Counting down ... 0    <level 5; final recursive call>
0: Kaboom!             <level 5; beginning to back out>
1: Kaboom!             <level 4>
2: Kaboom!             <level 3>
3: Kaboom!             <level 2>
4: Kaboom!             <level 1>
```

Note that each recursive call creates its own set of variables, so by the time the program reaches the fifth call, it has five separate variables called n, each with a different value. You can verify this for yourself by modifying Listing 7.16 so that it displays the address of n as well as its value:

```cpp
cout << "Counting down ... " << n << " (n at " << &n << ")" << endl;
...
cout << n << ": Kaboom!" << " (n at " << &n << ")" << endl;
```

Doing so produces output like the following:

```text
Counting down ... 4 (n at 0012FE0C)
Counting down ... 3 (n at 0012FD34)
Counting down ... 2 (n at 0012FC5C)
Counting down ... 1 (n at 0012FB84)
Counting down ... 0 (n at 0012FAAC)
0: Kaboom!           (n at 0012FAAC)
1: Kaboom!           (n at 0012FB84)
2: Kaboom!           (n at 0012FC5C)
3: Kaboom!           (n at 0012FD34)
4: Kaboom!           (n at 0012FE0C)
```

Note how the n having the value 4 is stored at one location (memory address 0012FE0C in this example), the n having the value 3 is stored at a second location (memory address 0012FD34), and so on. Also note how the address of n for a particular level during the “Counting down” stage is the same as its address for the same level during the “Kaboom!” stage.

## Recursion with Multiple Recursive Calls

Recursion is particularly useful for situations that call for repeatedly subdividing a task into two smaller, similar tasks. For example, consider this approach to drawing a ruler. Mark the two ends, locate the midpoint, and mark it. Then apply this same procedure to the left half of the ruler and then to the right half. If you want more subdivisions, apply the same procedure to each of the current subdivisions. This recursive approach is sometimes called the *divide-and-conquer strategy*. Listing 7.17 illustrates this approach, with the recursive function `subdivide()`. It uses a string initially filled with spaces except for a `|` character at each end. The main program uses a loop to call the `subdivide()` function six times, each time increasing the number of recursion levels and printing the resulting string. Thus, each line of output represents an additional level of recursion. To remind you that it’s an option, the program uses the `std::` qualifier instead of a using directive.

### Listing 7.17 **ruler.cpp**

```cpp
// ruler.cpp -- using recursion to subdivide a ruler
#include <iostream>
const int Len = 66;
const int Divs = 6;
void subdivide(char ar[], int low, int high, int level);
int main()
{
    char ruler[Len];
    int i;
    for (i = 1; i < Len - 2; i++)
        ruler[i] = ' ';
    ruler[Len - 1] = '\0';
    int max = Len - 2;
    int min = 0;
    ruler[min] = ruler[max] = '|';
    std::cout << ruler << std::endl;
    for (i = 1; i <= Divs; i++)
    {
        subdivide(ruler,min,max, i);
        std::cout << ruler << std::endl;
        for (int j = 1; j < Len - 2; j++)
            ruler[j] = ' ';  // reset to blank ruler
    }

    return 0;
}

void subdivide(char ar[], int low, int high, int level)
{
    if (level == 0)
        return;
    int mid = (high + low) / 2;
    ar[mid] = '|';
    subdivide(ar, low, mid, level - 1);
    subdivide(ar, mid, high, level - 1);
}
```

Here is the output of the program in Listing 7.17:

```text
|                                   |
|                       |           |
|           |           |           |
|     |     |     |     |     |     |
|  |  |  |  |  |  |  |  |  |  |  |  |
|||||||||||||||||||||||||||||||||||||
```

## Program Notes

The `subdivide()` function in Listing 7.17 uses the variable `level` to control the recursion level. When the function calls itself, it reduces the level by one, and the function with a level of 0 terminates. Note that `subdivide()` calls itself twice, once for the left subdivision and once for the right subdivision. The original midpoint becomes the right end for one call and the left end for the other call. Notice that the number of calls grows geometrically. That is, one call generates two, which generate four calls, which generate eight, and so on. That’s why the level 6 call is able to fill in 64 elements (2⁶ = 64). This continued doubling of the number of function calls (and hence the number of variables stored) make this form of recursion a poor choice if many levels of recursion are required. But it is an elegant and simple choice if the necessary levels of recursion are few.

## Pointers to Functions

No discussion of C or C++ functions would be complete without mention of pointers to functions. We’ll take a quick look at this topic and leave the full exposition of the possibilities to more advanced texts.

Functions, like data items, have addresses. A function’s address is the memory address at which the stored machine language code for the function begins. Normally, it’s neither important nor useful for you or the user to know that address, but it can be useful to a program. For example, it’s possible to write a function that takes the address of another function as an argument. That enables the first function to find the second function and run it. This approach is more awkward than simply having the first function call the second one directly, but it leaves open the possibility of passing different function addresses at different times. That means the first function can use different functions at different times.

## Function Pointer Basics

Let’s clarify this process with an example. Suppose you want to design an `estimate()` function that estimates the amount of time necessary to write a given number of lines of code, and you want different programmers to use the function. Part of the code for `estimate()` will be the same for all users, but the function will allow each programmer to provide his or her own algorithm for estimating time. The mechanism for that will be to pass to `estimate()` the address of the particular algorithm function the programmer wants to use. To implement this plan, you need to be able to do the following:

- Obtain the address of a function.
- Declare a pointer to a function.
- Use a pointer to a function to invoke the function.

## Obtaining the Address of a Function

Obtaining the address of a function is simple: You just use the function name without trailing parentheses. That is, if `think()` is a function, then `think` is the address of the function. To pass a function as an argument, you pass the function name. Be sure you distinguish between passing the *address* of a function and passing the *return value* of a function:

```cpp
process(think);   // passes address of think() to process()
thought(think()); // passes return value of think() to thought()
```

The `process()` call enables the `process()` function to invoke the `think()` function from within `process()`. The `thought()` call first invokes the `think()` function and then passes the return value of `think()` to the `thought()` function.

## Declaring a Pointer to a Function

To declare pointers to a data type, the declaration has had to specify exactly to what type the pointer points. Similarly, a pointer to a function has to specify to what type of function the pointer points. This means the declaration should identify the function’s return type and the function’s signature (its argument list). That is, the declaration should provide the same information about a function that a function prototype does. For example, suppose Pam LeCoder has written a time-estimating function with the following prototype:

```cpp
double pam(int);   // prototype
```

Here’s what a declaration of an appropriate pointer type looks like:

```cpp
double (*pf)(int);   // pf points to a function that takes
                     // one int argument and that
                     // returns type double
```

> **Tip**
> 
> In general, to declare a pointer to a particular kind of function, you can first write a prototype for a regular function of the desired kind and then replace the function name with an expression in the form `(*pf)`. In this case, `pf` is a pointer to a function of that type.
