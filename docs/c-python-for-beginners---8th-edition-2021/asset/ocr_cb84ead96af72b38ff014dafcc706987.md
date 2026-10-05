# STEP 5

You can assign a value to a variable as soon as you declare it. The code you've typed in could look like

```
int a = 10;
int b = 5;
int result = a + b;

cout << result;
```

# STEP 8

The previous step creates the variable StartLives, which is a global variable. In a game, a player's lives go up or down depending on how well or bad they're doing. When the player restarts the game, the StartLives returns to its default: 3. Here we have assigned 3 lines, subtracted 1, and leaves left:

```
C:\Users\david\Document\Variables.exe
Process returned (0) execution time 0:00
Press any key to continue.
```

![](bbox=[0.0615, 0.2565, 0.4855, 0.4035])

```
C:\Users\david\Document\Variables.exe
Process returned (0) execution time 0:00
Press any key to continue.
```

# STEP 6

Specific to C++, you can also use the following to assign values to a variable as soon as

```
int a (10);
int b (5);
```

Then, the C++ 2011 standard, using curly brackets:

```
int result {a+b};
```

![](bbox=[0.0615, 0.5435, 0.4855, 0.6935])

```
C:\Users\david\Document\Variables.exe
Process returned (0) execution time 0:00
Press any key to continue.
```

# STEP 9

The modern C++ is far more intelligent than most programmers give it credit. While there are declare for variables, you can use the auto feature:

> #include <iostream>
using namespace std;
auto pi = 3.141593;

```
int main() {
```

```
double area, radius = 1.5;
area = pi * radius;
cout << area;
```

![](bbox=[0.5145, 0.6135, 0.9385, 0.7635])

```
C:\Users\david\Document\Variables.exe
Process returned (0) execution time 0:00
Press any key to continue.
```

# STEP 7

You can create global variables, which are declared outside any function and used within the entire code. What you've used so far are local variables: variables used inside the function. For example:

> #include <iostream>
using namespace std;
StartLives = 3;

```
int main() {
```

```
StartLives = StartLives - 1;
cout << StartLives;
```

# STEP 10

A couple of new features here: first, auto won't work until you go to Settings -> Compiler and check the box labeled 'Have C++11 ISO C++ Language [-std=c++11]'. Then, the new data type, double, will build and run code. The result is 7.06858.

![](bbox=[0.5145, 0.8835, 0.9385, 0.9535])

www.bdmppublications.com 69