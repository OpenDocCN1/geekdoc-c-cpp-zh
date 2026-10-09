
## 1.6 Making decisions

Let's write a new program. Run through a similar process to that given above, but this time let's call our project **ExamCalculator**. Change all the folders accordingly. The code for the `main.cpp` file in this project should look like this:

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int mark;
    cout << "What was your average mark?\n";
    cin >> mark;

    if (mark >= 70) {
        cout << "Congratulations!\n";
        cout << "You got a distinction.\n";
    }
    else if (mark >= 60) {
        cout << "Well done!\n";
        cout << "You got a merit!\n";
    }
    else if (mark >= 50) {
        cout << "You passed.\n";
    }
    else {
        cout << "You failed :-(\n";
    }

    return 0;
}
```

Notice first that all of the boiler plate code is the same as in the last example. This is why I'm calling it boiler plate code. You can just copy it without thinking for the time being.

The more interesting thing to notice is that we are using an `if` statement to make decisions on what the code should do next. The code to be executed in each of the different circumstances is grouped together in sets of curly brackets.

Be careful to notice the round brackets in the condition to be tested.

The `else if` parts of the statement are optional as is the `else`. You can have as many `else if` statements as you like.

Strictly speaking, when you only have one statement in a group you can omit the curly brackets. For example, you could finish the code with just

```cpp
} else
    cout << "You failed :-\n";
return 0;
```

However, it is generally accepted that code with curly brackets throughout is easier to read. So you should always include them.

C++ doesn't care much where you put spaces in your code. However, if you space your code nicely it can be much easier to read. Different authors have different preferences for how to format curly brackets. We will write our curly brackets so that the \{ appears at the end of a line, the \} appears at the beginning of the line, and everything inside the brackets is indented. You will see different conventions in other books. It doesn't matter what convention you choose, but it does make your code more readable if you pick a convention and stick to it.

# 1.7 Exercises

1.7.1 If a company has revenue $r$ and costs $c$, then its gross profits, $g$, are given by $g = r - c$. If it has made a positive gross profit, suppose that a tax of $tg$ must be paid where $t$ is the tax rate. On the other hand, if the company has made a loss, no tax is payable. The net profit is equal to the gross profit with tax paid subtracted.

Write a program called **ProfitCalculator**, which prompts the user for the revenue, the costs, and the tax rate, and then prints out the gross profit and the net profit.

Write two versions, one using single letter variable names and one using long variable names such as **grossProfit**. Note that in C++ variable names can't contain spaces. This is why we use capitals in this way. This way of writing variable names as all one word with capitals in the middle is called *camel case*. The reason is because the word has now got a hump like a camel.

Do you prefer the code with long variable names or single letter names? Which of the two versions would be easier for someone else to understand?

# **1.8 Summary**

We have seen an example C++ program and learned how to compile and run it. We have learned how to work with the error messages produced by the compiler.

http://taylorandfrancis.com

# Chapter 2

## Basic Data Types and Operators

Whenever you use a variable in C++ you must specify the type of data that will be stored in that variable. Moreover, once you have chosen the type of data to be stored in a given variable you can’t change it. The jargon phrase is that it is a *statically typed language*. This distinguishes C++ from computer languages which take a more relaxed attitude to specifying the type of data.

The reason that specifying the type of data is important is that ultimately, data is stored on your computer data as strings of 1s and 0s. Integers are encoded as binary numbers. Letters are encoded as numbers written in binary. Floating point numbers are stored in a binary version of scientific notation.

The problem is that if you just look at the 1s and 0s without also knowing the type of the data, the data is completely meaningless. The chip that powers your computer’s processing (the CPU or Central Processing Unit) treats data blindly without caring about the type. This means that the CPU is willing to carry out some pretty silly computations if you ask it to. For example, you can ask your CPU to multiply the integer representing the character “w” by the number seven. Probably the only reason you would do this is if your code contains a bug and is accidentally using the same variable for numbers and letters. These kinds of bugs can be found before you ever even run your code if you use a statically typed language.

The C++ language has evolved from the C language. C is also statically typed.

One of the reasons C caught on in the first place is that it is statically typed. The machine-code everyone used before C came along was not statically typed. Programmers quickly found that the C compiler was able to find a lot of bugs automatically by checking types. This meant that they were able to spend more time writing new code and less time fixing bugs.

# **2.1** Memory terminology

Because data is stored on computers using 1s and 0s, it is natural to store integers using binary.

- A single binary digit is called a bit. This is just a truncation of the phrase binary digit.
- 8 binary digits are called a byte. This is just a bad joke.
- 1024 bytes make a kilobyte (1024 = 2^10 so the usual use of “kilo” to mean 1000 is tweaked to work better in binary).
- 1048576 = 2^20 bytes make up a megabyte.
- Numbers representing memory locations are often written in hexadecimal. This is base 16. The 16 characters 0, 1, 2, . . . , 9, A, B, C, D, E, and F are used to represent hexadecimal digits. So A is equivalent to the decimal number 10 and F to the decimal number 15. The hexadecimal number 10 can be written in decimal as 16. Four binary digits are equivalent to one hexadecimal digit. For this reason, one hexadecimal digit is called a nibble.

As is already clear, computer programmers have a particularly poor sense of humour.

> Old Joke: There are 10 kinds of people. Those who understand binary, and those who don’t.

# 2.2 Basic data types

## 2.2.1 Integers

You can assign a fixed value to a variable of type int using the = operator as follows.

```cpp
int numberOfPlatonicSolids = 5;
```

When you type an integer you should not include any commas or spaces. So don’t write 1,000,000, simply write 1000000.

If you like you can specify an integer using a different numeric base. For example, if you prefer counting in hexadecimal (base 16) you can type 0xFF instead of 255. The prefix 0x means “This number is in hexadecimal”.

Confusingly, the prefix 0 on its own means “This number is in base 8”. So the code

```cpp
int numberOfPlanets = 08;
```

doesn't compile. Unfortunately, the chances of you remembering this fact are slim! Fortunately, the chances of you making this error are also reasonably low.

When you add two integers, you get an integer, of course. Similarly, if you multiply or subtract them. However…

# Danger!

When you divide two integers in C++ you get another integer. C++ simply rounds down if necessary. The C++ code 3/5 evaluates to 0.

C++ actually gives you a number of choices for storing integer data depending on the potential range of values your variable might take. Here are some other data-type specifiers that are available, which all mean an integer of one form or another:

- short
- int
- long
- long long
- unsigned short
- unsigned int
- unsigned long
- unsigned long long
- size_t

The range of values you can store in each of these data types varies between different C++ compilers. As you might guess, you can store smaller numbers in shorts than you can in long longs. What you can be sure of is that you will be able to store a value between −2^31 and 2^31 − 1 in an int variable and a value between −2^63 and 2^63 − 1 in a long long variable.

By specifying that a variable is unsigned you are saying that it is non-negative. Specifying the sign of a number takes up one bit of memory, so unsigned integers can be twice as big as signed ones.

If you add one to an integer that takes the maximum possible value for that data type, C++ wraps the value round so that it now takes the minimum possible value for that data type. In other words, C++ does its computation in binary and simply discards the top digits if an integer overflows the possible range.

This isn't normally a problem in practice unless you decide to use the unsigned data types. For these data types you will find that the calculation 0 − 1 yields a number greater than 0. This is extremely confusing and leads to lots of bugs. For this reason I recommend that you avoid using the unsigned data types.

The type size_t is used to store the size of data structures stored in memory. Since the maximum amount of memory you can access on a 32-bit
