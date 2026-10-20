# STEP 5

You can assign a value to a variable as soon as you declare it. The code you’ve typed in could look like this, instead:

```
int a = 10;
int b = 5;
int result = a + b;

cout << result;
```

![](bbox=[0.065, 0.247, 0.49, 0.384])

# STEP 6

Specific to C++, you can also use the following to assign values to a variable as soon as you declare them:

```
int a (10);
int b (5);
```

Then, from the C++ 2011 standard, using curly brackets:

```
int result {a+b};
```

![](bbox=[0.065, 0.527, 0.49, 0.664])

# STEP 7

You can create global variables, which are variables that are declared outside any function and used in any function within the entire code. What you’ve used so far are local variables: variables used inside the function. For example:

```
#include <iostream>
using namespace std;
int StartLives = 3;

int main ()
{
    startLives = StartLives - 1;
    cout << StartLives;
}
```

![](bbox=[0.065, 0.872, 0.49, 0.938])

# STEP 8

The previous step creates the variable StartLives, which is a global variable. In a game, for example, a player’s lives go up or down depending on how well or how bad they’re doing. When the player restarts the game, the StartLives returns to its default state: 3. Here we’ve assigned 3 lives, then subtracted 1, leaving 2 lives left.

![](bbox=[0.51, 0.222, 0.935, 0.279])

# STEP 9

The modern C++ compiler is far more intelligent than most programmers give it credit. While there are numerous data types you can declare for variables, you can in fact use the auto feature:

```
#include <iostream>
using namespace std;
auto pi = 3.141593;

int main()
{
    double area, radius = 1.5;
    area = pi * radius * radius;
    cout << area;
}
```

![](bbox=[0.51, 0.522, 0.935, 0.683])

# STEP 10

A couple of new elements here: first, auto won’t work unless you go to Settings > Compiler and tick the box labelled ‘Have G++ follow the C++11 ISO C++ Language Standard [-std=c++11]’. Then, the new data type, double, which means double-precision floating point value. Enable C++11, then build and run the code. The result should be 7.06858.

![](bbox=[0.51, 0.795, 0.935, 0.938])