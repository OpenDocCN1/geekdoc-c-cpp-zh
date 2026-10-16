# # 150 ■ Programming in C++ for Engineering and Science

> > I never met a library I didn’t like.

A MAJOR THEME OF THIS CHAPTER is writing code that is reusable. As we show first, reusability may be on a “local” level in which code segments are encapsulated in a function that is a separate part of a program but can be used anywhere else in the program. Also, because it is a separate piece of code, it can be used in other programs by copying and pasting this code into them. For reusability on a larger scale, functions (and other program components such as constant declarations) can be stored in a library from which any program can retrieve and use them, just as the programs in Examples 5.4 and 5.5 used the function sqrt() from the cmath library.

A second theme of this chapter is information hiding, also known as abstraction, which refers to separating unnecessary details about a computation from what others need to know in order to use it. Here again we will see that this separation can be done on a local scale for functions that are part of a program, and that libraries make true information hiding possible.

Also, functions make it possible to modularize programs, which facilitates solving complex problems. We divide a problem into a number of simpler problems, develop functions to solve these simpler problems, and then combine them with a main “driver” program to produce a complete program that solves the original problem. In this chapter, however, we will look only at fairly simple functions in detail and give several examples, because understanding how to construct and use functions is fundamental to writing reusable code. We will also see how libraries are constructed. It must be realized, however, that this first look at functions and libraries is only an introduction. Many more features and uses will be given in later chapters.



Many problems involve the use of formulas in their solutions. For example, in Section 4.1, we used Einstein’s formula e = m × c² to compute the energy released by a quantity of matter and found that converting this formula into a C++ expression was quite straightforward. In this chapter we begin with a temperature-conversion problem that is also easy to solve in C++, but our first version of a program to perform these conversions will undergo a series of modifications with a view to increasing reusability.



Fahrenheit and Celsius are two scales used to measure temperature. We will develop a program to convert temperatures in Celsius to the equivalent Fahrenheit temperatures.





Our program will repeatedly display on the screen a prompt for a Celsius temperature. Each time, the user will enter a numeric value (the Celsius temperature) from the keyboard that the program will read. It will then compute the Fahrenheit temperature equivalent of