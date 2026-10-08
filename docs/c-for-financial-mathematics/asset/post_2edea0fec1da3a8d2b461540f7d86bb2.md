
The book has been designed for a 12-week course at the level of a UK financial mathematics MSc programme. For a shorter course, it would be natural to end at one of the following milestones.

- In Chapter 9 we price a call option using the Monte Carlo method. This gives a practical demonstration of the *procedural programming* skills learned in previous chapters.
- In Chapter 13 we price a portfolio of derivatives using the Monte Carlo method. Since there should be no restrictions on the derivatives that might be in the portfolio, this makes heavy use of *object-oriented* programming.
- In Chapter 18 we extend our model to include markets with multiple stocks. This requires us to use some more interesting data structures and showcases more advanced techniques such as templates and operator overloading.
- In Chapter 20 we show how multiple threads can be used to speed up Monte Carlo calculations. This demonstrates how the C++ techniques described in the book can be combined to build a sophisticated project.

Finally, in Chapter 21 we give some suggestions for further reading and give some general suggestions for possible programming projects to build on the skills you developed by this book.

## Acknowledgements

I am indebted to Plamen Turkedjiev, Soheli Rahman, and Alice Sullivan for their many contributions to this book.

## Summary

This book provides an introduction to the C++ language and the art of writing high-quality code in that language.

We will illustrate these computer skills with financial examples, specifically the problem of pricing a portfolio of derivatives.

# Chapter 1

## Getting Started

We start by learning how to write and run a simple example program to compute compound interest. First we will need to install and configure the software required to write C++ programs. Next we will see how to write a simple program.

### 1.1 Installing your development environment

You will need to install some sort of *development environment* on your computer in order to write C++ programs. A development environment is rather like a word processor, except it allows you to write software rather than documents. Just as with word processors, there are quite a few different development environments you can choose from. We will give some recommendations that have been tested to work with this course.

#### 1.1.1 For Windows

You will need to download Microsoft Visual Studio Express for Windows Desktop[^1]. This software is freely available.

[^1]: https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx

#### 1.1.2 For Unix

If you are using Unix you will need a text editor and the programs **g++** and **make**. If they are not already installed, follow the instructions for your Unix distribution, which you should be able to readily find online. Another program you should install is **gdb**, which we will discuss in Chapter 15.

#### 1.1.3 For MacOS X

Install Apple's XCode[^2] development environment.

[^2]: http://developer.apple.com/technology/xcode.html

## 1.2 Running an example program

Let us start with an example program. Don’t worry what it does for now. The first thing we need to do is work out how to run it.

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
	// Interesting code starts
	int principal;
	double interestRate;
	int numberOfYears;
	
	cout << "How much are you investing?\n";
	cin >> principal;
	cout << "What’s the annual interest rate (%)?\n";
	cin >> interestRate;
	cout << "How long for (years)?\n";
	cin >> numberOfYears;
	
	double finalBalance = 
		pow(1.0 + interestRate * 0.01, numberOfYears) 
		* principal;
	double interest = finalBalance - principal;
	
	cout << "You will earn ";
	cout << interest;
	cout << "\n";
	/* Interesting code ends */
	return 0;
}
```

You can also find this code on the website of the book[^3]. Follow the link for the project “InterestCalculator” for Chapter 1.

[^3]: <http://www.routledge.com/cw/armstrong>

### 1.3 Compiling and running the code

Running C++ code isn't as easy as you might like. The reason for this is that C++ is what is called a “compiled language”.

The chip inside a computer that does most of the work is called the CPU (central processing unit). It does not know the C++ language or indeed any computer language which is pleasant to program in. The CPU speaks a language called assembly language, also known as machine code. In machine code, all instructions are coded up as a sequence of numbers. Each number is a code word for some action the CPU should take. Programming in machine code directly is completely unbearable. What is worse, different CPUs may use different versions of assembly language, so you have to rewrite your code for different computers.

To get around this, one programs in “higher level languages” which are written in ways that humans can understand. At some point, the program’s instructions need to be converted to machine code.

In an “interpreted” language, the instructions are converted to machine code every time they are executed. MATLAB and Python are examples of interpreted languages.

In a “compiled” language, the instructions are converted to machine code before the program is ever run. This process is called compilation. C++ is a compiled language, so you must compile your code before you can run it.

Historically, the advantage of compiled languages was that they run faster. The reason for this is that converting things to machine code takes time. If you do this every time the code is run, it will necessarily run slower. The big disadvantage was that you have to recompile your code if you change the type of computer you want to run it on.

These days, computers are so fast that this advantage is not really relevant any more. Modern languages can be compiled very fast and even use “just in time compilers” that observe how the software is being used by the user and perform optimisations based on this. This is one of the reasons why the claim C++ is faster than languages such as Java and C# is a bit of a myth.

A good development allows you to compile and then run your code at the touch of a button. But before we can do this, we need to get our code into our development environment.

We will now describe the steps you need to go through to compile the example code. Jump to the relevant section for your computer and follow the instructions to the letter. Note that a guide to compiling on Macs can be found on the website accompanying this book.

You will need to get everything exactly right. If you cannot get the code to work, there is a zip file called InterestCalculator on the website for this book. This contains working versions of the code that you can use.

#### 1.3.1 Compiling on Windows

- Open Visual Studio.
- Select **File→New→Project...**
- Select **Empty→Project**
- Enter the Name `InterestCalculator` and press **OK**.
- Note the name of the folder where your project is being saved.
- Notice that to the right of the screen you have an area marked **Solution Explorer** inside which there is a picture of a folder marked **Source Files**. Right click on this and select **Add→New item...
- Select the option “C++ file” and enter the name `main.cpp` and press Add.
- This creates a file called `main.cpp` which we will use to store our code. On the right-hand side of the screen you will see a text editor window where you can edit the code for `main.cpp`.
- Copy and paste the example code from the website[^4] into the editor window.
- Select **Project→Interest Calculator Properties...**, then select **Linker→System** and set the `SubSystem` to `Console (/SUBSYSTEM:CONSOLE)` using the drop down.
- Press **OK**
- Press `CTRL` + `F5` to compile and run your program

This should have worked if you have managed to follow every instruction exactly. If it fails, close Visual Studio, delete all the files in the directory you noted down and try again! But this time be more careful.

Setting up your first-ever project is probably the most fiddly and tedious task you will have to perform in this book.

Why are there so many steps to creating your project?

Firstly a typical C++ project contains a lot of different files, so in practice you don’t normally run through such a complex process very often. Most of the steps above are only needed when you create a new project. The two steps that you would be likely to perform repeatedly are:

- (i) creating new C++ source files by right clicking on the **Source Files** folder;
- (ii) pressing `CTRL` and `F5` to compile and run your program.

[^4]: http://www.routledge.com/cw/armstrong
