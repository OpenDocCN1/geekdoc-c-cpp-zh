
When you run this application, you see the following output:

```
10.5
10.5
```

In this code, you use a function or machine called `fabs()` (usually pronounced "ef-abs," for floating-point absolute). This function takes a number as input and returns as output the absolute value of the number.

![](img/128ab511de4e7360e167e3b15cdd5dd0_162_0.png)

The absolute value of a number is simply the positive version of the number. The absolute value, for example, of -5 is simply 5. The absolute value of 12 is still 12. An absolute value is almost always positive because the absolute value of 0 is 0, but 0 is the origin, which is neither positive nor negative (see http://www.math.com/school/subject1/lessons/S1U1L10DP.html for details). The reason for the f before the name abs is that it uses floating-point numbers, which are simply numbers with decimal points.

So the first line inside `main()` calls `fabs()` for the value -10.5. The cout then takes the output of this function (that is, the result) and prints it to the console.

Then the second line does the same thing again, except that it takes the absolute value of the number 10.5.

And where is the processor for this function? It's not in your code; it's in another file, and the following line ensures that your application can use this function:

```
#include <math.h>
```

You have seen functions in many places. If you use a calculator and enter a number and press the square root button, the calculator runs a function that calculates the square root.

But functions can be more sophisticated than just working with numbers. Consider this statement carefully: When you are using a word processor and you highlight a word and check the spelling of the word, the application calls a function that handles the spelling check. This function does something like the following:

```
This is a function to check the spelling of a single word.
Inputs: A single word.
Look up the word
If the word is not found
    Find some suggestions.
    Open a dialog box through which you (the user)
        can change the word by either typing a new word
or picking one of the selections, or just leaving
it the same.
If you made a change,
    Return the new spelling.
Otherwise
    Return nothing.
Otherwise
    Return nothing
```

## Dividing Your Work with Functions

Notice how the `if` statements are grouped with indentations. The final `otherwise` goes with the first `if` statement because its indentation matches that of the `if` statement.

So that’s a function that performs a spelling check. But consider this: When you do not highlight a word but run the spelling checker, the spelling checker runs for the whole document. That’s another function. Here it is.

```
This function checks the spelling of the entire document
For each word in the document
    Check the spelling of the single word
```

How does the computer do the step inside the `for` loop, “Check the spelling of the single word?” It calls the function described earlier. This process is called *code reuse*. You have no reason to rewrite the entire function again if you already have it somewhere else. And that’s the beauty of functions.

### Calling a Function

When you run the code in a function, computer people say that you are *calling* the function. And just like every good person, a good function has a name. When you call a function, you do so by name.

![](img/128ab511de4e7360e167e3b15cdd5dd0_163_0.png)

Often, when writing an application and developing code to call a function, developers say that they are calling a function. This is partly computerspeak and partly a strange disorder in which developers start to relate just a little too much to the computer.

To call a function, you type its name and then a set of parentheses. Inside the parentheses, you list the items you want to send to the inputs of the function. The term used here is *pass*, as in “You pass the values to the function.”

### Using Auto for Functions

In general, specifically defining the type of the variable you use to receive output from a function makes your code more readable. However, there are situations for which you may not know the precise output type or different versions of the function output different types (which is very confusing). In this case, you begin by setting GCC to use C++17, as described in the "Working with ranges" section of Book 1, Chapter 5. Then, you can write the Fabs2 example shown in Listing 6-2, as shown in the following UsingAuto example:

```cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
{
    auto mynumber = fabs(-23.87);
    cout << mynumber << endl;
    return 0;
}
```

The result is the same as the Fabs2 example. The difference is that mynumber is now of type auto, where C++ automatically detects the data type for you, instead of double, where you explicitly define the data type.

### Passing a variable

You can also pass the value of a variable into a function. The Fabs3 example in Listing 6-3 creates two variables: One is passed into the function, and the other receives the result of the function.

- **LISTING 6-3:** Seeing Yet Another Way to Use fabs()

```cpp
#include <iostream>
#include <math.h>

using namespace std;

int main()
{
    double start = -253.895;
    double finish = fabs(start);
    cout << finish << endl;
    return 0;
}
```

This code creates two variables; the first is called `start`, and the second is called `finish`. It initializes `start` with a value of -253.895. Next, it calls `fabs()`, passing it the value of `start`. It saves the return value in `finish`, and prints the value in `finish`. When `fabs()` runs, you see the following appear on the console:

```text
253.895
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_166_0.png)

Saving a function result to a variable is useful if you need to use the result several times over. For example, if you need the absolute value of −253.895 for whatever reason and then a few lines later you need it again, you have a choice: You can either call `fabs(-253.895)` each time or call it once, save the result in a variable, and then use the variable each time you need it. The advantage to saving it in a variable is that you might later say, for example, “Oh, wait! I didn’t just want the absolute value! I wanted the negative of the absolute value!” Then you only have to change one line of code — the line where it calls `fabs()`. If, instead, you had called `fabs()` several times, you would have had to change it every time you called it. And by the way, in case you’re curious about how to take the negative of the absolute value and store it in a variable, you just throw a minus sign in front of it, like so:

```cpp
finish = -fabs(start);
```

### Passing multiple variables

Some functions like to have all sorts of goodies thrown your way, such as multiple parameters. As with functions that take a single value, you put the values inside a single set of parentheses. Because you have multiple values, you separate them with commas. The `pow()` example, shown in Listing 6–4, uses a function called `pow()` to calculate the third power of 10. (That is, it calculates 10 times 10 times 10. Yes, `pow()`.) Make sure that you include the math.h line in the `#include` section so that you can use the `pow()` function.

### Defining the AddOne() function

The AddOne example, shown in Listing 6–5, provides both a custom function and code in main() that calls the custom function. (The function is placed outside main() — before it, in fact.)

- **LISTING 6-5:** Writing Your Very Own Function

```cpp
#include <iostream>

using namespace std;

int AddOne(int start)
{
    int newnumber = start + 1;
    return newnumber;
}

int main()
{
    int testnumber = 20;
    int result = AddOne(testnumber);
    cout << result << endl;
    return 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_168_0.png)

Notice that this example lacks the `#include <math.h>` entry found in earlier examples. You need to add an entry to the include section of your code only when you use a feature of that include file. In this case, the example relies on standard math features that are part of the basic C++ language, so you don’t need any additional code.

Using the downloadable source will save you time and ensure that the example runs the first time you try it. However, you might choose to type it manually. Because there’s a good bit of code, you may get some compiler errors at first; look carefully at the lines with the errors and find the difference between your code and what’s here in the book. After you run the example, you see:

```
21
```
