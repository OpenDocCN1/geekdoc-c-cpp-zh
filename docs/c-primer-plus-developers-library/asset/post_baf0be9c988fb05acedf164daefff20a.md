
Suppose you want to add a second user-defined function. Just as with a library function, you can call a user-defined function by using its name. And, as with a library function, you must provide a function prototype before using the function, which you typically do by placing the prototype above the `main()` definition. But now you, not the library vendor, must provide source code for the new function. The simplest way is to place the code in the same file after the code for `main()`. Listing 2.5 illustrates these elements.

### Listing 2.5 `ourfunc.cpp`

```cpp
// ourfunc.cpp -- defining your own function
#include <iostream>
void simon(int);   // function prototype for simon()

int main()
{
    using namespace std;
    simon(3);       // call the simon() function
    cout << "Pick an integer: ";
    int count;
    cin >> count;
    simon(count);   // call it again
    cout << "Done!" << endl;
    return 0;
}

void simon(int n)  // define the simon() function
{
    using namespace std;
    cout << "Simon says touch your toes " << n << " times." << endl;
}                 // void functions don't need return statements
```

The `main()` function calls the `simon()` function twice, once with an argument of 3 and once with a variable argument count. In between, the user enters an integer that’s used to set the value of count. The example doesn’t use a newline character in the `cout` prompting message. This results in the user input appearing on the same line as the prompt. Here is a sample run of the program in Listing 2.5:

```text
Simon says touch your toes 3 times.
Pick an integer: 512
Simon says touch your toes 512 times.
Done!
```

## Function Form

The definition for the `simon()` function in Listing 2.5 follows the same general form as the definition for `main()`. First, there is a function header. Then, enclosed in braces, comes the function body. You can generalize the form for a function definition as follows:

```text
type functionname(argumentlist)
{
    statements
}
```

Note that the source code that defines `simon()` follows the closing brace of `main()`. Like C, and unlike Pascal, C++ does not allow you to embed one function definition inside another. Each function definition stands separately from all others; all functions are created equal (see Figure 2.8).

![](img/9afc44517b591d64e2e19f623c9308ef_69_0.png)

Figure 2.8 Function definitions occur sequentially in a file.

## Function Headers

The `simon()` function in Listing 2.5 has this header:

```cpp
void simon(int n)
```

The initial `void` means that `simon()` has no return value. So calling `simon()` doesn’t produce a number that you can assign to a variable in `main()`. Thus, the first function call looks like this:

```cpp
simon(3);          // ok for void functions
```

Because poor `simon()` lacks a return value, you can’t use it this way:

```cpp
simple = simon(3);   // not allowed for void functions
```

The `int n` within the parentheses means that you are expected to use `simon()` with a single argument of type `int`. The `n` is a new variable assigned the value passed during a function call. Thus, the following function call assigns the value 3 to the n variable defined in the `simon()` header:

```cpp
simon(3);
```

When the `cout` statement in the function body uses n, it uses the value passed in the function call. That’s why `simon(3)` displays a 3 in its output. The call to `simon(count)` in the sample run causes the function to display 512 because that was the value entered for count. In short, the header for `simon()` tells you that this function takes a single type int argument and that it doesn’t have a return value.

Let’s review `main()`’s function header:

```cpp
int main()
```

The initial int means that `main()` returns an integer value. The empty parentheses (which optionally could contain `void`) means that `main()` has no arguments. Functions that have return values should use the keyword return to provide the return value and to terminate the function. That’s why you’ve been using the following statement at the end of `main()`:

```cpp
return 0;
```

This is logically consistent: `main()` is supposed to return a type int value, and you have it return the integer 0. But, you might wonder, to what are you returning a value? After all, nowhere in any of your programs have you seen anything calling `main()`:

```cpp
squeeze = main();    // absent from our programs
```

The answer is that you can think of your computer’s operating system (Unix, say, or Windows) as calling your program. So `main()`’s return value is returned not to another part of the program but to the operating system. Many operating systems can use the program’s return value. For example, Unix shell scripts and Windows command-line interface batch files can be designed to run programs and test their return values, usually called *exit values*. The normal convention is that an exit value of zero means the program ran successfully, whereas a nonzero value means there was a problem. Thus, you can design a C++ program to return a nonzero value if, say, it fails to open a file. You can then design a shell script or batch file to run that program and to take some alternative action if the program signals failure.

## Keywords

Keywords are the vocabulary of a computer language. This chapter has used four C++ keywords: `int`, `void`, `return`, and `double`. Because these keywords are special to C++, you can’t use them for other purposes. That is, you can’t use `return` as the name for a variable or `double` as the name of a function. But you can use them as part of a name, as in `painter` (with its hidden int) or `return_aces`. Appendix B, “C++ Reserved Words,” provides a complete list of C++ keywords. Incidentally, `main` is not a keyword because it’s not part of the language. Instead, it is the name of a required function. You can use `main` as a variable name. (That can cause a problem in circumstances too esoteric to describe here, and because it is confusing in any case, you’d best not.) Similarly, other function names and object names are not keywords. However, using the same name, say, `cout`, for both an object and a variable in a program confuses the compiler. That is, you can use `cout` as a variable name in a function that doesn’t use the `cout` object for output, but you can’t use the `cout` both ways in the same function.

## Using a User-Defined Function That Has a Return Value

Let’s go one step further and write a function that uses the return statement. The `main()` function already illustrates the plan for a function with a return value: Give the return type in the function header and use `return` at the end of the function body. You can use this form to solve a weighty problem for those visiting the United Kingdom. In the United Kingdom, many bathroom scales are calibrated in *stone* instead of in U.S. pounds or international kilograms. The word *stone* is both singular and plural in this context. (The English language does lack the internal consistency of, say, C++.) One stone is 14 pounds, and the program in Listing 2.6 uses a function to make this conversion.

### Listing 2.6 `convert.cpp`

```cpp
// convert.cpp -- converts stone to pounds
#include <iostream>
int stonetolb(int);      // function prototype
int main()
{
    using namespace std;
    int stone;
    cout << "Enter the weight in stone: ";
    cin >> stone;
    int pounds = stonetolb(stone);
    cout << stone << " stone = ";
    cout << pounds << " pounds." << endl;
    return 0;
}

int stonetolb(int sts)
{
    return 14 * sts;
}
```

Here’s a sample run of the program in Listing 2.6:

```text
Enter the weight in stone: 15
15 stone = 210 pounds.
```

In `main()`, the program uses `cin` to provide a value for the integer variable `stone`. This value is passed to the `stonetolb()` function as an argument and is assigned to the variable `sts` in that function. `stonetolb()` then uses the `return` keyword to return the value of `14 * sts` to `main()`. This illustrates that you aren’t limited to following `return` with a simple number. Here, by using a more complex expression, you avoid the bother of having
