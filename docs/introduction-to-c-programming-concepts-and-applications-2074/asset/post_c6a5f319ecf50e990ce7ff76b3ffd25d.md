
# // BUILDING A LIBRARY

If you're going to have a library, you're going to want a namespace—the name and double colon that you have to put in certain commands—help you separate the functions in your library from others.

In the main function, you can call the greeting function by writing english::greeting() (14). That means you can call the function named greeting within the english namespace. When that is called, Hello! is printed out.

The header file will contain the namespace, any variables to be defined in that library or namespace, and the function declarations—which are just part of the header file, not including the braces.

You should be familiar with the using namespace std that you've been putting at the beginning of every program, enabling you to use commands in the standard namespace std:: in front of everything.

Just like libraries such as iostream provide useful functions, you can create your own libraries in a similar way. When you create your own library, you will want to put all of the new functions in a separate namespace to prevent any overlap in the naming of different functions.

The declaration is a way of saying "there will be a function with this signature" not actually saying how function is implemented. The actual implementation is the definition.

Namespaces are a way of helping distinguish one library's functions from another. That way, if you have a function named get_data, then another library can also have a function get_data. They can be in different namespaces, and the 2 functions remain distinct.

When you separate libraries and as wanting to write really large programs—the types that are built by teams of people or one person working a long time—you can begin to make use of a feature called separate compilation.

Up until this, you've been putting the definition with the declaration, as is common in one file. But the header-like and the body-like definition can be split up. If you want to try this, you'll probably need to use an IDE like Visual Studio or Xcode rather than an online browser-based compiler. See page 172 for instructions on how to separate source and header files in your.

You can also create your own namespaces. To do this, you use the keyword namespace and then the name you want to use for your namespace; then, in curly braces, you include all the declarations that will be part of that namespace.

Suppose you want to create a library of functions. The common practice in C and C++ is to break the code for these into two files: header file and source file. Header files have a .h or sometimes a .hpp file extension, while source files have a

```
// Program 15_3
// Namespace example
#include <iostream>
using namespace std;
namespace english {
void greeting() {
    cout << "Hello!" << endl;
}
}
int main() {
    english::greeting();
}
```

For example, in Program 15_3, you have a namespace named english (1). Inside the curly braces, you define a function that is of type named greeting (m). This function is defined as part of the namespace.

Lecture 15 | Functions in Top-Down and Bottom-Up

When designing your program, using pseudocode to look out your functions, look at all of them and search for places where you want to reuse the code. Or a file might seem to have too many ideas in one place. Both are good times to consider breaking functions into separate files.

- Dividing functions across files helps ensure that no single file is too large and everything in one file is closely related.
- By separately compiling files, only the files that are recompiled. On large projects, that can greatly improve productivity.

There are many reasons why separate compilation is useful, particularly for larger tasks.

- It makes it easier to reuse files in other programs; you write the code once and then just #include in it other programs.

In fact, you could separately compile every function you write. But for beginners, this makes a code harder to handle, and you will not be able to execute code from the browser-based development environment. The rule of thumb is to consider separation when you might reuse code or to simplify files. 🔸

## HOW TO CREATE SEPARATE SOURCE AND HEADER FILES IN YOUR IDE

In Visual Studio, the separate files you create are not automatically put in your project, so you will have to add files to the project when you're ready to compile them. To add your separate files to the project:

- Save the files.
- Go to the project window and select “add” and “existing item”.
- Add all 3 files to the project:
- the source file that contains main
- the header file that contains the function header
- the source file that contains the function definition
- Then, you can build the project: run it.

## READINGS

- Stroustrup, Programming Principles and Practice Using C++, 8.7 for (namespaces).
- Lippman, Lajo, and Moo, C++ Primer, section 18.2 (for namespaces).
- Csterhouse, A Philosophy of Software Design, chap. 4 (describing design) and chap. 5 (describing information hiding).
- See references from lecture 11: Problem Solving and Program Design in C (8th ed.) by Jeri R. Hanly and Elliott B. Koffman and Problem Solving, Abstract, and Design Using C++ (6th ed.) by Frank Lied and Elliott B. Koffman.

Xcode automates putting the files in the project.

- Start with the main.cpp file, with main automatically repeating.
- Go to the File menu and create a Header File.
- Save it as .h.
- Save it as a C++ file, .cpp.
- If you create the .cpp source file first, Xcode will give you the option of also creating the header file automatically.
- Build and Run the program.

# // QUIZ

1 Match the idea to its name:

2 Imagine you have the following program and want to break it into several files, which will be compiled separately. Specifically, you would like to have: a library header file, a library implementation file, and a main file. Which of the code would end up in each of these files?

- a top-down
b bottom-up
c separate compilation
d stub
namespace
affold

1 a way of building a program by combining existing, simpler parts

2 a way of writing a minimal function that it can be called when testing some other code

```
#include <iostream>
using namespace std;
bool update_balance(float& balance, float payment, float interest) {
    balance -= payment;
    if (balance <= 0) {
        return true;
    }
    balance *= (1.0+interest/100.0);
    return false;
}
int main() {
    float account_balance=1000.0;
    float payment = 50.0;
    float interest_rate = 3.5;
    int numpments = 1;
    while (update_balance(account_balance,payment,interest_rate)) {
        numpments++;
        payment += 10.0;
    }
    cout << "It takes " << numpments << " increasing payments to pay the balance in the account." << endl;
}
```

3 a way of setting up code so that a particular function can be tested

4 a way of grouping functions and variables with a common purpose

5 a way of dividing a program into multiple files

6 a way of dividing a problem into simpler subproblems

# // QUIZ ANSWERS

- 1 Separate compilation means that functions can be placed in separate files that are compiled separately. In this case, that means that there will be the following:

- b 1

>> a header file, containing the function header:

```
bool update_balance(float& balance, float payment, float interest)
```

>> an implementation file, containing the function definition:

```
bool update_balance(float& balance, float payment, float interest) {
balance -= payment;
if (balance <= 0) {
    return true;
}
balance *= (1.0+interest/100.0);
return false;
}
```

>> a main file that would include the main program (it must also #include the library header file):

```
int main() {
    float account_balance=1000.0;
    float payment = 50.0;
    float interest_rate = 3.5;
    int numpayment = 1;
    while(update_balance(account_balance,payment,interest_rate)) {
        numpayment++;
        payment += 10.0;
    }
    cout << "It takes " << numpayment << " increasing payments to pay the balance in the account." << endl;
}
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_179_0.png)
