
Arguments that will be sent to the function, and the return type that will be returned. The definition of a function, on the other hand, will be supplied in the body of any function that we want to build. The standard library that we encounter with this language will supply us with several already usable and callable functions.

For example, one of them is the strcat() method, which can be used to concatenate two strings, and then you may use the memcpy() function to assist us in moving memory from one area to another. These are only a handful of the functions you may use, and they all operate in the same manner. So, let's have a look at how C++ functions will operate.

## It is best defined as follows:

```cpp
return_type function_name(parameter list)
{
    body of the function
}
```

The definition of the functions we have here will include a header for the function as well as its body.

Some of the several function aspects that we will need to examine are as follows:

- **1. The return type:** In certain circumstances, when we use a function, it will return some kind of value to us. When this occurs, we will use the return type to ensure that something is returned to us. Some of our functions will be able to do the activities you want without delivering value to you. With the syntax we described above, you would receive a value back, however, it would be "void."
- **2. Function name:** Now we may deal with the function name. When you're finished, you'll be able to give your function a name and a parameter. You will also get what is known as the function signature.
- **3. Parameters:** The parameters will just serve as a type of placeholder to deal with. When you're ready to call one of your functions, just assign the value to one of the arguments. This value will be referred to as the argument or real parameter. The parameter list may then refer to the order, number, and type of arguments that are sent to the function. In rare circumstances, it is feasible to operate with a function that lacks these arguments entirely.
- **4. Body of function:** Finally, let's have a look at the function body. This will have a decent collection of statements that will inform us what the function is capable of doing. While we're here, we may as well go through this and deal with something called function overloading. This implies that the C++ language will enable us to assign two or more definitions to the name of a function or one of our operators inside the same scope.

Depending on which one we do this to, this will be termed as operator overloading or function overloading.

An overloaded declaration is just one that is declared with the same name as the previous declaration, as long as they are in the same scope. The exception to this is that both of the declarations we have here will have distinct arguments and will have different definitions and implementations from one another. When we call one of the overloaded operators or functions, the compiler will be able to look at all of the definitions and decide which one is the best to utilize. It does this by comparing the various kinds of arguments used to invoke the operator or function, and it can also operate with the types of parameters stated in the definitions. This is a large procedure that the compiler will have to deal with. The good news is that we will be able to see the correct results each time, as long as we set up the software correctly.

Overload resolution is the process of identifying the most suitable function that has been overloaded. As previously stated, we may go through and have many definitions for the same function even though we are using the same scope. Our function definitions must vary from one another, either in terms of the type or the number of parameters present in one of our lists of arguments. Remember that overloading the declaration of our function is not permitted if the only difference is the return type.

Even though it may seem to be tough at first, working with this overloading of functions is rather simple.

A nice example of the code that we can use to make this happen is seen below, where the print() function is used to assist us to print out all of the various forms of data.

```cpp
#include <iostream>
using namespace std;

class printData {
   public:
      void print(int i) {
         cout << "Printing int: " << i << endl;
      }
      void print(double f) {
         cout << "Printing float: " << f << endl;
      }
      void print(char* c) {
         cout << "Printing character: " << c << endl;
      }
};

int main(void) {
   printData pd;

   // Call print to print integer
   pd.print(5);

   // Call print to print float
   pd.print(500.263);

   // Call print to print character
   pd.print("Hello C++");

   return 0;
}
```

When we finish compiling this one and can go through and run it properly, it will provide us with some results based on the sorts of data that we contributed to it. When dealing with operator overloading in C++, we may use a similar procedure. We can go through and overload or rewrite several of the C++ language's built-in operators.

As a result, the application will be allowed to employ operators with certain of their user-defined types if that is their preference. To make things simple, the overloaded operators will be functions with unique names. Typically, this will contain the term "operator," followed by the symbol corresponding to the operator that you want to specify here.

The operator that you are attempting to overload, like any of the other functions that you are utilizing, will come with both the return type and our parameter list.

## How to Deal with Exceptions

One of the cool things about what we can accomplish with the C++ language is that it is designed to manage things like exceptions. This is a little more difficult, but you'll be astonished at some of the various codes we can use with it.

An exception, as we shall define it here, is an issue that will appear when you are ready to run your program, indicating that it will not operate correctly.

When we look into exceptions in C++, we will see that this is what will happen in response to an uncommon scenario in the code, which will often appear when we execute and run the program. The most typical form of exception that we will see in our code and programs is when someone attempts to divide by zero. Exceptions will be a valuable component to have in your code since they will assist us in transferring some of the control that is present in one part of the program and ensuring that it is transferred to one of the other sections.

The C++ exception handling is going to be based on some of the core keywords, namely a try, throw, and catch. Let's look at what these terms signify to gain a better grasp of why they're essential and what we can do with them:

- **1. Throw:** The first of these keywords will be referred to as a throw. When an issue occurs, the software will throw an exception. When we use the throw keyword, this will happen automatically.
- **2. The catch:** A program will be able to detect one of the exceptions with the aid of an exception handler, which will allow the program to address some of the issues on its own. If you use the catch keyword, it will take some time to inform your application that you want it to catch that exception.
- **3. Try:** When we are ready to use the try keyword, we will do so to assist us to find and identify the blocks of code where a specific exception will be triggered.

If you use this keyword, it will contain at least one catch block to ensure that it works.

We will then assume that your present block may throw an exception and that a method will be able to catch the exception using a combination of the catch and try keywords. These will then be included in the code, allowing it to catch the exception and handle it for you. This is not a guarantee that an exception will occur, but if it is possible, putting these in will ensure that the code continues to behave as it should. As we can see, many distinct pieces will come together to help us build the fundamental grammar of our C++ code. You may utilize as many of these sections as you like along the way to ensure that the coding works properly, even though some of the fundamental codes you start with may only require one or two of them to function properly. Learning these fundamentals and how to write programs correctly will make all the difference as we go through this manual and beyond with this coding language.
