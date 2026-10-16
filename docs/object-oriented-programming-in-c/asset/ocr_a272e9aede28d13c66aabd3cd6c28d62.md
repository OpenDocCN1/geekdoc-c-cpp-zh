+   (b) In C++, a function contained within a class is called a member function.
+   (c) Looking at one or two lines of code, we can easily recognize whether a program is written in C or C++.
+   (d) In C++, it is very easy to add new features to the existing structure of an object.
+   (e) The concept of using one operator for different purposes is known as operator overloading.
+   (f) The output function printf() cannot be used in C++ programs.

2.2 Why do we need the preprocessor directive #include <iostream> ?

2.3 How does a main() function in C++ differ from main() in C?

2.4 What do you think is the main advantage of the comment // in C++ as compared to the old C type comment?

2.5 Describe the major parts of a C++ program.

# Debugging Exercises

2.1 Identify the error in the following program.

```
#include <iostream.h>
void main()
{
    int i = 0;
    i = i + 1;
    cout << i << " ";
    /*comment\*/ // i = i + 1;
    cout << i;
}
```

2.2 Identify the error in the following program.

```
#include <iostream.h>
void main()
{
    short i=2500, j=3000;
    cout >> "i + j = " >> (i+j);
}
```

2.3 What will happen when you run the following program?

```
#include <iostream.h>
void main()
{
```