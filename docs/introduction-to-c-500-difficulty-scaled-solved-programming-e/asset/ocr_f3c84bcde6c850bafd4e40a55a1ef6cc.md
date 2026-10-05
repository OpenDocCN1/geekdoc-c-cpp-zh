# 206 Introduction to C++

```
int main()
{
    float (*ptr)(float a, float b); /* ptr is declared as a pointer to a
    function, which takes two float parameters and returns a float. */
    float i, j, max;

    std::cout << "Enter grades: ";
    std::cin >> i >> j;

    ptr = test;
    max = (*ptr)(i, j); // Call the function that ptr points to.
    std::cout << "Max:" << max << '\n';
    return 0;
}
```

```
float test(float a, float b)
{
    if(a > b)
        return a;
    else
        return b;
}
```

We could omit the declaration of max and write: cout << "Max:" << (i, j) << '\n';

# Function Pointers as Arguments

You may possibly wonder, isn't this section so specialised, am I ever going to pass a function pointer to a function? You're right, I'd probably wonder the same if I were in your place and skip that section. However, it is almost certain that you need this knowledge in several cases such as to call a library function that accepts a parameter or to enable the communication of different parts of your program.

Let's discuss about second case. Several applications need a part of the program (e.g., B) to notify another part (e.g., A) for the emergence of event. To achieve this, a function of part A calls a function of part B and passes it a pointer to a function in part A. The function in part B copies pointer into a variable and variable is used by part B to notify part A for some event. This communication mechanism is known as callback mechanism. For example, in one of my applications, part B was the controller of a serial port and used that callback mechanism to notify the main program (part A) to receive data. Let's see a coding example of this mechanism:

```
#include <iostream> // Example 8.25
#include <cstdlib>
#include <ctime>
```

```
void make_rand(*ptr)(int evt, int num); /* Although we could write make-
rand(void ptr(int evt, int num)); I prefer to use the pointer notation. */
void handle_event(int evt, int num);

int main()
{
    srand(time(NULL));
    make_rand(handle_event);
    return 0;
}
```