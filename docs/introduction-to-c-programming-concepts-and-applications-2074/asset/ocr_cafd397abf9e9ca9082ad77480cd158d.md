# // VARIABLE DECLARATIONS

A computer's main working memory is made up of many locations, each of which is capable of storing just 1 or 0. However, programmers do not write in machine language.

So, programming languages let you take a section of that memory, which of Os, and use for your own purposes. This section of memory is called a **variable**. Think of a variable as a box that can hold different values—that is, you can change it whenever you want.

In C++, in order to use a variable, you first have to declare it. In other words, you write your program instruction to the computer that says,"I want to set aside a box of memory for me to use as a variable."That operation—saying you want a particular variable—is called **variable declaration**.

# RULES FOR NAMING VARIABLES

+   Names to begin with a letter. Besides letters, it's also possible to start with the underscore character, but you should not do this, because it is usually reserved for special types in the compiler that come up in more advanced systems programming.

+   As for the rest of the name, you can use letters, underscore characters, or numbers.

+   There are a few special words in C++, often called **keywords** or reserved words, that are used for other things, so you can't use them. For example, you cannot name a variable **namespace** or **using**. There are also a few predefined identifiers, as **main**, that would be possible to declare that you should just avoid in your own variable names.

The **variable name** is what you'll refer to the box of memory. This variable name is often called the identifier, because it identifies which box of memory you are referring to. When you use `carb_grams` in your program, you are referring to that box of memory—and, more specifically, to the value contained in that box of memory.

that's just a bunch of 1s and Os would be a pain to deal with—if you had to write in the 1s and Os of binary.

Every variable declaration needs two things: a **type** and a **name**. For example, you could declare an integer variable that you name **year**. The code for the code would be `int year;` where `int` is short for integer—any counting number, such as 0, 1, or 12.

The way you get the ability to write variables in a form you understand is with the variable type. When you declare a variable, you first tell the computer what type of that variable will be.

In the calorie-counting program, the line `int carb_grams (7)` gives the pieces of information you need to declare a variable: the type of (**int**) and the variable name (**carb_grams**).

Next, the next line of code (8) is another variable declaration. You're telling the computer:"Set aside a box of integer-type memory called **protein_grams.",

In the example (**Program 2_1 on page 18**), the type is **int**, which means the programmer can think of it as containing an integer. The computer will handle the converting of integer to binary format. As you just say that you want a box of memory and declare the type of data that will be in.

Every variable declaration sets aside a box of memory, which will have one value inside of it. But setting aside a box of memory

Lecture 02 | Variables, Computations, and Input in C++