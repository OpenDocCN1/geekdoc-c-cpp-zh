
The phrase `double interestRate;` means: "please make room in memory for a variable called `interestRate` that will store a real number". There are two keywords you can use in C++ to store a real number. You can use `float` which stores a floating point number to a certain precision, or you can use `double` which uses twice as much memory but is much more precise. Computer memory is cheaper now than it was in 1969, so `float` isn’t used much any more. The strange name `double` lives on for backwards compatibility. If you think of `double` as meaning "real number" you won’t get into much trouble.

Notice the semi-colon at the end of the statement `int principal;`. Every statement in C++ ends with a semi-colon. You can think of it as the C++ equivalent of a full stop in English. However, C++ is much fussier than the English language—if you forget a single semi-colon, the program won’t work.

The line

```cpp
cout << "How much are you investing?\n";
```

writes the text "How much are you investing?" to the screen and then starts a new line. Anything enclosed in quotation marks is interpreted as text rather than computer code by C++. The special sequence of characters `\n` means insert a new line.

The line

```cpp
cin >> principal;
```

means read a number typed by the user and store it in the variable `principal`.

The next few lines behave much the same.

The mathematical heart of our calculation is given by the lines:

```cpp
double finalBalance = 
        pow(1.0 + interestRate * 0.01, numberOfYears)
        * principal;
double interest = finalBalance - principal;
```

These lines make room in memory for two variables called `finalBalance` and `interest` and immediately assign values to these variables.

The computation of the interest is simple. It is just the `finalBalance` minus the `principal`.

The final balance is computed using the formula $P(1 + i)^T$ where $P$ is short for `principal`, etc. Our code just expands the variable names, replaces multiplication with `*`, and uses the function `pow` to raise a number to a given power. In general `pow(a,b) = a^b`.

Notice that C++ doesn’t care if your statements go over multiple lines. This is great if you want to write a long formula. The price you have to pay is that you must end all statements with a semi-colon, since C++ doesn’t look at the spacing of your code to guess where one statement ends and another begins. We have indented our code to indicate that the first three lines should be read as a group. You should always space your code carefully to make it easy to read.

Unlike many other languages, C++ doesn't have a special symbol for raising a number to a given power. You might think that the symbol ^ would be a good choice, but C++ in its wisdom uses that for another purpose.

Notice that in mathematics we normally use single letters for variable names such as the formula $P(1 + i)^T$. When writing software, it is usually better to use long variable names. This is because you can then just read the code without having to go somewhere else to find what all the letters stand for.

The next few lines should now be self-explanatory. They print out the answer.

```cpp
cout << "You will earn ";
cout << interest;
cout << "\n";
```

This example shows why C++ makes you specify the line breaks by hand: Sometimes it can be useful to print out only part of a line.

The last few lines are more boiler plate:

```cpp
    return 0;
}
```

If you are curious about what the boiler plate code means, don't worry. All will be explained shortly.

## Exercises

One of the most difficult parts of learning C++ is learning how to cope with compiler errors. So this section is very important. I recommend you refer back to it whenever an error happens in your code.

The exercises below show what actually happens if we make some small mistakes in our code.

1.  **1.4.1.** In the line

    ```cpp
    int principal;
    ```

    remove the semi-colon and then compile the code (recall that on Visual Studio that means press **CTRL F5** and on Unix you should type **make all**). What error message is reported? Do you find this error message helpful?

    Note that if you are working on Windows, you will have to use the scroll bar to move the text in the **Output** window to the right. Better yet, find the button on the toolbar of the **Output window** to enable word wrap. Examine the error message. What part of it do you find most helpful? Can you see how the compiler reports which line contains the error? Has it got this right?

    Put the semi-colon back, and make sure you can compile and run the code once again.

2.  **1.4.2.** Repeat the exercise above but removing the `)` symbol in the calculation of the final balance instead. Make sure you get everything working again before moving onto the next exercise.

3.  **1.4.3.** Repeat the exercise above but removing the `{` symbol at the end of the line

    ```cpp
    int main() {
    ```

    Don't panic! Just fix the problem.

4.  **1.4.4.** Repeat the exercise above, but this time instead of just deleting a character, insert a whole new first line of code that just contains the letter x. Thus the code should start

    ```cpp
    x
    #include <iostream>
    ```

    Don't panic! Just fix the problem.

5.  **1.4.5.** As well as compilation errors, code can contain programming errors that the compiler does not spot. Arguably our example contains one already. What happens if you type “1000$” as the amount you would like to invest? This happens because our code assumes you will only type in numbers.

6.  **1.4.6.** What error do you get if you completely delete the line `int principal;`? This happens because before you can use a variable in C++ you must tell the compiler what type the variable is.

## Tip: Dealing with compilation errors

C++ is very sensitive to tiny punctuation errors. When you get a screen full of errors, don't panic just: **scroll up to the first error, fix that, and try again.**

Once C++ is confused it starts misinterpreting all of your code completely.

So one tiny error can look like a disaster. This is why you should only ever try and fix one error at a time.

You should treat the error messages as the compiler's best guess of what you've got wrong. As the examples above show it can get both the line numbers wrong and the description of the error wrong.

In particular the line number might be slightly below the actual line containing an error, or if you are really unlucky it might think the error is in a different file. The line numbers reported as containing errors actually mark the points where it *realised* that there was an error. This is why they are often below where the real error occurred.

If the compiler tells you that the error is not in your code but in a library it has definitely got it wrong!

You will find it very hard to work out where you have made an error in your code. So always write programs a couple of lines at a time, constantly testing that they compile and run. Then you *know* that any error that appears must be in the lines you've just written.

If you made the mistake of writing an enormous chunk of code and can't work out where the errors are, then delete it all (or comment it out) and put it back piece by piece. Learn from your mistake and start writing code a little bit at a time.

## 1.5 Configuring the compiler

We have given a detailed recipe for how to configure the compiler to run a simple program. If you are working on Windows, you will see that there are many available options that we are ignoring. Similarly on Unix our Makefile sets some basic compiler options, but other options are available.

We won't worry much about configuring the compiler in this book as it is an advanced topic which only becomes important if you are building large programs that use different libraries or if you want to make sure the code is fully optimised.

We have chosen to configure the compiler so that if errors occur when the program is running, the error messages should be a bit more helpful. We call this “debug mode”. Alternatively it is also possible to configure the compiler so that it runs as fast as possible. When developing code, or when learning programming for the first time, it is a good idea to prioritise helpful error messages. Once you are happy with your code, you might want to compile it again with different settings so that it runs more quickly. This final version of your code is called the “release” version of your code because it is the version you would release to any users.
