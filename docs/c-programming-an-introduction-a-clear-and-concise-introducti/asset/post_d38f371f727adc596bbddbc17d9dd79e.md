
```cpp
void addFive(int &num)
{
    num += 5;
}
```

Some programmers suggest placing the ampersand by the data type instead of the parameter, but the compiler accepts either style.

Parameters should only be passed by reference when there is no other way to accomplish the particular task. For example, the addFive() function above could just as easily be written with a value parameter that returns the parameter plus 5 to the calling program, so that the variable passed as a parameter can be assigned the return value of the function. Or in clearer code terms:

```cpp
int addFive(int num)
{
    return num += 5;
}

// in calling program
int number = 0;
number = addFive(number);
```

However, there are situations when only passing parameters by reference will do, and the swap() function is one of those situations. The main reason we have to write the function with reference parameters is because a value-returning function can only return a single value, but the swap() function is working with two values.

With no further ado, let's rewrite the swap function so that it works correctly:

```cpp
void swap(string &word1, string &word2)
{
    string temp = word1;
    word1 = word2;
    word2 = temp;
}
```

The variables word1 and word2 are now passed by reference, so that when the function changes the values of the variables, it is really changing them in the calling program as well as in the function. Here is the complete program again:

```cpp
// Swap.cpp : main project file.

#include "stdafx.h"

using namespace System;

#include <iostream>
#include <string>
using namespace std;

void swap(string &word1, string &word2)
{
    string temp = word1;
    word1 = word2;
    word2 = temp;
}

int main(array<System::String ^> ^args)
{
    string word1, word2;
    word1 = "banana";
    word2 = "apple";
    cout << word1 << " " << word2 << endl;
    swap(word1, word2);
    cout << word1 << " " << word2 << endl;
    Console::ReadKey();
    return 0;
}
```

The output looks like this:

```
banana apple
apple banana
```

The values stored in the respective memory addresses have now been swapped so that word1 stores "apple" and word2 stores "banana".

## Variable Scope

The scope of a variable refers to the accessibility of a variable. How and where a variable is accessible depends on where the variable is declared. It is best to explain how variable scoping works through examples. Look at this simple program fragment:

```cpp
int main()
{
    int number1;
    number1 = 23;
    int number2 = number1 * 13;
    return 0;
}
```

The scope of the variable number1 is the main() function. Any and all code within the main() function's block can access the value of number1. Now look at this next longer code fragment:

```cpp
int changeNumber(int number)
{
    return number *= 3;
}

int main()
{
    int number = 3;
    cout << changeNumber(number);
    cout << number;
    return 0;
}
```

The parameter number is said to be local to the function changeNumber(). What this means is that this variable is accessible only to code within the function definition, and once the function stops executing, its value is completely removed from memory.

To demonstrate how this works, let's rewrite the program above to demonstrate how local scope works. The complete program is listed below:

```cpp
// ScopeExample.cpp : main project file.

#include "stdafx.h"

using namespace System;
#include <iostream>
using namespace std;

int changeNumber(int number)
{
    number *= 3;
    cout << "The value of number in the changeNumber()"
         << " function is: " << number << endl;
```

## Levels of Scope

The example above illustrates one of the levels of scope available in a C++ program. These scope levels are:

- *Global*
- *Local*
- *Block*

Variables declared within a function, either the main function or a user-defined function, have local scope. The variable and the variable's value are accessible to any code written within the block that defines the function. Code from another function does not have access to that variable.

## Global Scope

A variable has global scope if it is defined in the global area of a C++ program. This area is the area where functions are defined, which includes the areas both above and below the main() function. A variable that is defined in this area is called a *global variable* and is accessible by any code in the program.

Let's look at a simple example of how global variables work:

```cpp
// GlobalScope.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int number = 1; // global variable

int changeNumber()
{
    number += 5;
    return number;
}

int main(array<System::String ^> ^args)
{
    cout << "The value of number is: " << number
         << endl;
    number = changeNumber();
    cout << "Now the value of number is: "
         << number << endl;
    Console::ReadKey();
    return 0;
}
```

The variable number is a global variable. The function changeNumber() has access to number's value even though the variable isn't passed to the function as an argument. Also, the main() function has access to number's value even though number isn't declared in the main() function.

As stated above, global variables are accessible by any code defined in the program. So you might think that you should declare all your variable as global to make it easy to work with them. That is the wrong idea, however. There are many problems with using global variables in your programs. These problems include:

- Unintentional changes – You might accidentally make a change to a global variable in one function and assume it has been unchanged in another function.
- Inability to reuse code – The heavy use of global variables makes your code more inflexible, making the code unusable in other programs.
- Inability to manage modularity – Code that makes heavy use of global variables is not as modular as code that uses more local variables.

The best advice is to start out making your variables local and then change them to global only when it is absolutely necessary. Later in this book we will discuss situations where using global variables is advantageous.

## Local Scope

We have already discussed how to create variables with *local scope* and will only review the concept here. Variables declared within the body of a function, including the main() function, are considered to have local scope. A variable with local scope has a lifetime that mirrors the lifetime of the function and any code defined in the body of the function that includes the declaration of the function has access to the variable.

## Block Scope

A variable that has *block scope* is accessible only to code found within the block of that variable. This may seem confusing since local variables are usually defined within a block, but there are many instances when there is a block of code within another block of code.

Consider the following simple for loop:

```cpp
// BlockScope.cpp : main project file.
#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    for(int i = 1; i <= 10; ++i)
    {
        cout << "The value of i in the loop is: "
             << i << endl;
    }
    Console::ReadKey();
    return 0;
}
```

The output from this program is:

```
The value of i in the loop is: 1
The value of i in the loop is: 2
The value of i in the loop is: 3
The value of i in the loop is: 4
The value of i in the loop is: 5
The value of i in the loop is: 6
The value of i in the loop is: 7
The value of i in the loop is: 8
The value of i in the loop is: 9
The value of i in the loop is: 10
```

Now, let's examine the value of i outside of the loop by adding this line right after the closing brace of the loop:

```cpp
cout << "The value of i outside the loop is: " << i
     << endl;
```

Now compile the program. You'll discover that you can't because there is an error. The error states that i is an undeclared identifier. That is because i is declared within the block of the for loop and has block scope. In other words, i and its value are only accessible within the for loop's block and once the for loop ends, the variable i is removed from memory.

You can use block-level scoping with any type of block. We haven't addressed this yet, but you can put a block of code anywhere in a program. Look at the following program:

```cpp
// BlockScope.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number = 1;
    cout << "The value of number is: " << number
         << endl;
    {
        int number = 100;
        cout << "The value of number in this block"
             << " is: " << number << endl;
    }
    number += 4;
    cout << "The value of number is: " << number << endl;
    Console::ReadKey();
    return 0;
}
```
