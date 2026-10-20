
## Loops and
Decision Making

Loops and repetition are one of the most important factors of any programming language. Good use of a loop creates a program that does exactly what you want it to and delivers the desired outcome without issues or errors.

Without loops and decision making events within the code, your program will never be able to offer the user any choice. It’s this understanding of choice that elevates your skills as a programmer and makes for much better code.

- 126 While Loop
- 128 For Loop
- 130 Do... While Loop
- 132 If Statement
- 134 If... Else Statement

## While Loop

A while loop’s function is to repeat a statement, or a group of statements, while a certain condition remains true. When the while loop starts, it initialises itself by testing the condition of the loop and the statements within, before executing the rest of the loop.

### TRUE OR FALSE?

While loops are one of the most popular form of C++ code looping. They repeatedly run the code contained within the loop while the condition is true. Once it proves false, the code continues as normal.

### STEP 1

Clear what you’ve done so far and create a new C++ file. There’s no need for any extra headers at the moment, so add the standard headers as per usual:

```
#include <iostream>
using namespace std;

int main ()
{
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_125_0.png)

### STEP 2

Create a simple while loop. Enter the code below, build and run (we’ve added comments to the screen shot):

```
{
    int num = 1;
    while (num < 30 )
    {
        cout << "Number: " << num << endl;
        num = num +1;
    }
    return 0;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_125_1.png)

### STEP 3

First you need to create a condition, so use a variable called num and give it the value 1. Now create the while loop, stating that as long as num is less than 30, the loop is true. Within the loop the value of num is displayed and adds 1 until it’s more than 30.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_125_2.png)

### STEP 4

We’re introducing a few new elements here. The first are the opening and closing braces for the while loop. This is because our loop is a compound statement, meaning a group of statements; note also, there’s no semicolon after the while statement. You now also have return 0, which is a clean and preferred way of ending the code.

```
int num = 1; // Create the condition
while (num < 30) // The condition remains true while num is less than 30
{
    cout << "Number: " << num << endl; // Displays the current value of num
    num = num +1; // Adds 1 to the value of num
}
return 0; // Correctly closes the code and finishes the program
```

### STEP 5

If you didn’t need to see the continually increasing value of num, you could have done away with the compound while statement and instead just added num by itself until it reached 30, and then displayed the value:

```
{
    int num = 1;
    while (num < 30 )
        num++;
    cout << "Number: " << num << endl;
    return 0;
}
```

### STEP 6

It's important to remember not to add a semicolon at the end of a while statement. Why? Well, as you know, the semicolon represents the end of a C++ line of code. If you place one at the end of a while statement, your loop will be permanently stuck until you close the program.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_126_0.png)

### STEP 7

In our example, if we were to execute the code the value of num would be 1, as set by the int statement. When the code hits the while statement it reads that while the condition of 1 being less than 30 is true, loop. The semicolon closes the line, so the loop repeats; but it never adds 1 to num, as it won't continue through the compound statement.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_126_1.png)

### STEP 8

You can manipulate the while statement to display different results depending on what code lies within the loop. For example, to read the poem, Cimmeria, word by word, you would enter:

```
#include <iostream>
#include <fstream>
using namespace std;

int main ()
{
    string word;
    ifstream newfile ("C:\\users\\david\\Documents\\Cimmeria.txt");

    cout << "Cimmeria, by Robert E Howard: \n" << endl;

    while (newfile >> word)
    {
        cout << word << endl;
    }

    return 0;
}
```

### STEP 9

You can further expand the code to enable each word of the poem to appear every second. To do so, you need to pull in a new library, <windows.h>. This is a Windows only library and within it you can use the Sleep() function:

```
#include <iostream>
#include <fstream>
#include <windows.h>
using namespace std;

int main ()
{
    string word;
    ifstream newfile ("C:\\users\\david\\Documents\\Cimmeria.txt");

    cout << "Cimmeria, by Robert E Howard: \n" << endl;

    while (newfile >> word)
    {
        cout << word << endl;
        Sleep(1000);
    }

    return 0;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_126_2.png)

### STEP 10

Sleep() works in milliseconds, so Sleep(1000) is one second, Sleep(10000) is ten seconds and so on. Combining the sleep function (along with the header it needs) and a while loop enables you to come up with some interesting countdown code.

```
#include <iostream>
#include <windows.h>
using namespace std;

int main ()
{
    int a = 10;

    while (a != 0)
    {
        cout << a << endl;
        a = a - 1;
        Sleep(1000);
    }

    cout << "\nBlast Off!" << endl;

    return 0;
}
```

## For Loop

In some respects, a for loop works in a very similar way to that of a while loop, although it’s structure is different. A for loop is split into three stages: an initialiser, a condition and an incremental step. Once set up, the loop repeats itself until the condition becomes false.

### LOOPY LOOPS

The initialise stage of a for loop is executed only once and this sets the point reference for the loop. The condition is evaluated by the loop to see if it’s true or false and then the increment is executed. The loop then repeats the second and third stage.

### STEP 1 Create a new C++ file, with the standard headers:

```
#include <iostream>
using namespace std;

int main ()
{ 
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_127_0.png)

### STEP 2 Start simple and create a for loop that counts from 1 to 30, displaying the value to the screen with each increment:

```
{ 
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
    {
        cout << "Number: " << num << endl;
    }
    
    return 0;
}
```

### STEP 3 Working through the process of the for loop, begin by creating an integer called num and assigning it a value of 1. Next, set the condition, in this case num being less than 30. The last stage is where you create the increments; here it’s the value of num being added by 1.

```
{ 
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
```

### STEP 4 After the loop, you created a compound statement in braces (curly brackets), that displays the current value of the integer num. Every time the for loop repeats itself, the second and third stages of the loop, it adds 1 until the condition <30 is false. The loop then ends and the code continues, ending neatly with return 0.

```
{ 
    //For Loop Begins
    for( int num = 1; num < 30; num = num +1 )
    {
        cout << "Number: " << num << endl;
    }
    
    return 0;
}
```

### STEP 5 A for loop is quite a neat package in C++, all contained within its own brackets, while the other elements outside of the loop are displayed below. If you want to create a 10-second countdown, you could use:

```
#include <iostream>
#include <windows.h>
using namespace std;

int main ()
{
    //For Loop Begins
    for( int a = 10; a != 0; a = a -1 )
    {
        cout << a << endl;
        Sleep(1000);
    }
    
    cout << "\nBlast Off!" << endl;
    
    return 0;
}
```

### STEP 6

With the countdown code, don’t forget to include the windows.h library, so you can use the Sleep command. Build and run the code; in the command console you can see the numbers 10 to 1 countdown in one second increments, until it reaches zero and Blast Off! appears.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_0.png)

### STEP 7

Naturally you can include a lot more content into a for loop, including some user input:

```
int i, n, fact = 1;
cout << "Enter a whole number: ";
cin >> n;
for (i = 1; i <= n; ++i) {
    fact *= i;
}
cout<< "\nFactorial of "<< n <<" = "<< fact << endl;
return 0;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_1.png)

### STEP 8

The code from step 7, when built and run, asks for a number, then displays the factorial of that number through the for loop. The user’s number is stored in the integer n, followed by the integer i which is used to check if the condition is true or false, adding 1 each time and comparing it to the user’s number, n.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_2.png)

### STEP 9

Here’s an example of a for loop displaying the multiplication tables of a user inputted number. Handy for students:

```
{
    int n;
    cout << "Enter a number to view its times table: ";
    cin >> n;
    for (int i = 1; i <= 12; ++i) {
        cout << n << " x " << i << " = " << n * i << endl;
    }
    return 0;
}
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_3.png)

### STEP 10

The value of the integer i can be expanded from 12 to whatever number you want, displaying a very large multiplication table in the process (or a small one). Of course the data type within a for loop doesn’t have to be an integer; as long as it’s valid, it works.

```
for ( float i = 0.00; i < 1.00; i += 0.01)
{
    cout << i << endl;
}
return 0;
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_128_4.png)
