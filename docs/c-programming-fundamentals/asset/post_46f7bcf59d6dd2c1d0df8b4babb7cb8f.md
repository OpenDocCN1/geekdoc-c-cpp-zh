
**Table 1.2 C++ Data Types and Domain Range**

| Data Type | Bytes | Range |
|---|---:|---|
| int | 4 | -2,147,483,648 to 2,147,483,647 |
| short int | 2 | -32,768 to 32,767 |
| long int | 4 | -2,147,483,648 to 2,147,483,647 |
| unsigned int | 4 | 0 to 4,294,967,295 |
| signed char | 1 | -128 to 127 |
| unsigned char | 1 | 0 to 255 |
| float | 4 | ±3.4E-38 and ±3.4E+38 |
| double | 8 | ±1.7E-308 and ±1.7E+308 |
| long double | 12 | ±1.7E-308 and ±1.7E+308 |

## 1.5 C++ Execution Flow

Let’s talk about a few basic terms before we move on:

- *Machine code* is instructions that only the computer understands, written in binary (0,1), and can be directly executed by a CPU.
- *Assembly code* is a low-level language consisting of statements written in English that can be understood by the programmer.
- *Debugging* means finding the faults or errors in your program to fix them so the program executes correctly.

A program in C++ executes in four stages, where different tools help us to make the execution process easier:

1. *Pre-processor*

   The first event that occurs in a C++ program is that the pre-processor processes the program before compilation. It includes the header files and any macros, if defined. It prepares the source code for the later stages of execution.

2. *Compiler*

   Now the pre-processed source code passes through the compiler to produce an object file. The compiler translates the programming language code in C++ into the machine language, and checks for any errors, issuing warnings about the errors. The object file contains the assembly code.

3. *Linker*

   The linker connects the libraries and object files together to generate an executable file with the extension .exe.

4. *Loader*

   The loader places your program onto the memory and this is where the program actually runs.

![](img/4d9a4ae4efedabe01be6e6c44bad2dc1_28_0.png)

*Figure 1.8* C++ execution flow

Let us write our first program in C++.

Steps to follow:

1. Get a text editor (such as Notepad) to write C++ code and a compiler (GCC) to translate the C++ code into machine code.
2. Get an IDE (Integrated Development Environment) to edit and compile your code (such as Code::Blocks, Eclipse, or, in this example, Visual Studio).
3. In Visual Studio, go to `File > New > File`, save the file (`new.cpp`) before you start coding.
4. Click on the right-most run symbol, which shows you options to debug or run the file to get output on the code terminal.

![](img/4d9a4ae4efedabe01be6e6c44bad2dc1_28_1.png)

*Figure 1.9* Visual Studio code options

5. Another way to run code is to type it into Notepad and then save it as a `.cpp` file. Open your command prompt terminal and type the `gcc filename.cpp` command to see output.

### Hello New You Program

### Code: First C++ Program

```cpp
#include <iostream> // preprocessor
using namespace std; // libraries used

int main() { // first block that runs
    //
    cout << "Hello new you!!"; // your first output
    return 0; // as the main method not void
}
```

### Output:

```text
Hello new you!!
```

## Summary

- C++ is a compiled, general-purpose, case-sensitive, and free-form programming language that supports procedural, object-oriented programming.
- C++ was developed by Bjarne Stroustrup in 1980 at Bell Labs.
- There are programming paradigms, such as procedural, structural, and object-oriented.
- C++ has OOP features, such as polymorphism, inheritance, data encapsulation, abstraction, message passing, and late binding.
- We learned about C++ data types, data modifiers, and variables.
- We looked at the ranges for `int`, `char`, and `long int`.
- We discussed working with a compiler and debugger.
- We considered the stages of C++ program execution.
- We wrote our first program in C++ using simple steps.

## Exercises

### Theory Questions

1. What are the features of C++? Why do we need to learn C++?
2. List four practical field applications of C++.
3. Differentiate between types of programming paradigms.
4. Explain OOP concepts with valid examples.
5. List the rules for naming a variable. Identify the valid variable names from the following list:
   - a. `_thisis2`
   - b. `24Hours`
   - c. `Name@dune`
   - d. `Formula1`
   - e. `___aditi`
   - f. `Meine#Name`
6. What are the tools used in C++ program execution?
7. Differentiate between compiler and debugger?
8. How exactly does a C++ program execute?

### MCQ-Based

1. Who is the original creator of the C++ language?
   - a. Dennis Ritchie
   - b. Ken Thompson
   - c. Bjarne Stroustrup
   - d. Brian Kernighan

2. C++ is a ___ type of language.
   - a. high-level
   - b. low-level
   - c. middle-level
   - d. None of the above

3. Which of the following symbols can be used to name a valid variable?
   - a. %
   - b. _
   - c. *
   - d. All of the above

4. Structure is what kind of data type?
   - a. Built-in
   - b. Derived
   - c. User-defined
   - d. None of the above

5. Which of the following features are supported by C++?
   - a. Encapsulation
   - b. Inheritance
   - c. Polymorphism
   - d. All of the above

6. What value does void hold?
   - a. Not defined
   - b. Null
   - c. 0
   - d. None of the above

7. Inside a class, the declared data members are known as ________
   - a. data
   - b. object and data
   - c. members
   - d. None of the above

8. What is the output of the following C++ program?

   ```cpp
   #include <iostream>
   using namespace std;
   int main ( )
   {
       double i;
       i = 15;
       cout << sizeof(i);
       return 0;
   }
   ```

   - a. 2
   - b. 3
   - c. 4
   - d. 8

9. The declaration of a variable means to ________ it?
   - a. introduce
   - b. delete
   - c. give value to
   - d. use

10. Object-oriented programming employs a ________ programming approach.
    - a. top-down
    - b. procedural
    - c. bottom up
    - d. All of the above

### Practical Application

1. Write a program in C++ to check the upper and lower limits of an integer.
2. Write a program in C++ to print your name and details on separate lines.
3. Write a program in C++ to find the size of the following variable: abc.
4. Write a program in C++ to find the sizes of various data types and print them.
5. Write a program in C++ to display the use of naming variables and their types.
6. Write a program in C++ to check whether variable 234Mine exists.

### MCQ

**Answer Key**

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|
| (c) | (c) | (b) | (c) | (d) | (b) | (c) | (d) | (a) | (c) |

## References

### Books

- B. Stroustrup, *The C++ Programming Language* (4th Edition), (Addison-Wesley Professional, 2013).
- K. R. Venugopal, *Mastering C++* (2nd Edition), (McGraw Hill Education, July 2017).
- Y. Kanetkar, *Let Us C++*, (BPB Publications, September, 2020).

### Websites

- Learn CPP, accessed May 2022, https://www.learncpp.com
- Silly Codes, accessed May 2022, https://sillycodes.com
- Codes Cracker, accessed May 2022, https://codescracker.com
- Geeks For Geeks, accessed May 2022, https://www.geeksforgeeks.org
- Udacity, accessed May 2022, https://www.udacity.com
- Scaler, accessed May 2022, https://www.scaler.com
- C Plus Plus, accessed May 2022, https://cplusplus.com

## Chapter 2: Basic Play in C++

### 2.1 Literals, Constants, and Qualifiers

Often while coding, your program will need a value that will not change throughout the program’s life, such as the value of pi or any basic values you wish not to manipulate. A fixed value that may not be changed is called a *constant*. Literal constants (or just *literals*) are unnamed values used directly in our code. They are constants because their values cannot be changed until you rewrite the program and compile it again. Just like objects have a type, all literals have a type. The type of a literal is assumed from the value and format of the literal itself. *Character literals* are enclosed in single quotes. A character literal can be a plain character, escape sequence, or universal character. A special character with a `\` at its beginning has a specific meaning and performs a certain function.
