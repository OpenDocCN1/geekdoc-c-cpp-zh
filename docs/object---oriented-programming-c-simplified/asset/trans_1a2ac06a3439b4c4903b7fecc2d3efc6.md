

# OUTPUT :

Enter no of elements <= 20
6
Enter 6 elements
60 10 30 20 45 25
Given array is
60 10 30 20 45 25
Sorted array is :
10 20 25 30 45 60

![](img/ad5299318df8d4d7c6df5eaa86590ea3_757_0.png)

Figure 15.33.Output screen of the program.

# Experiment-10 : Write programs illustrating file handling operations :

+   (a) Copying a text file
+   (b) Displaying the contents of the file, etc.

# /*PROGRAM : READING AND WRITING MOBILE DETAIL */

```
#include <iostream.h>
#include <fstream.h>
void main()
{
    fstream rw;
    rw.open("demo2.txt",ios ::out);
    char mcomp[20],model[10];
    float price;
    cout<<"Enter the mobile model"<<endl;
    cin.getline(model, 10);
    cout<<"Enter the mobile company"<<endl;
    cin.getline(mcomp, 20);
cout<<"Enter the mobile price"<<endl;
cin>>price;
rw<<model<<endl<<mcomp<<endl<<price<<endl;
rw.close();
rw.open("demo2.txt",ios::in);
rw.getline(model,10);
rw.getline(mcomp,20);
rw>>price;
cout<<"Mobile details read from file"<<endl;
cout<<"Model :="<<model<<endl;
cout<<"Company :="<<mcomp<<endl;
cout<<"Price :="<<price<<endl;
rw.close();
}
```

# OUTPUT :

Enter the mobile model
z550i
Enter the mobile company
Sony
Enter the mobile price
8000
Mobile details read from file
Model :=z550i
Company :=Sony
Price :=8000

![](img/ad5299318df8d4d7c6df5eaa86590ea3_758_0.png)

Figure 15.34. Output screen of program.

![](img/ad5299318df8d4d7c6df5eaa86590ea3_760_0.png)

**Figure 15.35.** *Output screen of program.*

**EXPLANATION :** We input source and destination file name from the user. It is assumed that source file exist so we have not put any error checking code in the program. The source file is than opened in read mode and destination file is in write mode. We read one character at a time from source file and put this into destination file. This continues till source file does not come to end. In the end both files are closed.

# KEY ELEMENTS USED IN
TROUBLE FREE C++

+   1. & has a number of distinct meanings. When it precedes the name of a variable without following the name of a type, it means “the address of the following variable”. For example, & Str means “the address of the variable Str”. When & follows a type name and precedes a variable name, it means that the variable being declared is a reference—that is, another name for a preexisting variable. In this book, references are used only in argument lists, where they indicate that the variable being defined is a new name for the caller’s variable rather than a new local variable.
+   2. % is the “modulus” operator, which returns the remainder after dividing its left-hand argument by its right-hand argument.
+   3. :: is the scope resolution operator, which is used to tell the compiler the scope of a variable. We can prefix it to the name of a global variable to prevent the compiler from confusing it with a variable of the same name from the standard library. It is also used to specify the namespace or class of a variable or function, when placed between the namespace or class name and the variable or function name.
+   4. < is the “less than” operator, which returns the value true if the expression on its left has a lower value than the expression on its right; otherwise, it returns the value false. Also see operator < in the index.
+   5. << is the “stream output” operator, used to write data to an ostream. Also see operator << in the index.¹
+   6. <= is the “less than or equal to” operator, which returns the value true if the expression on its left has the same or a lower value than the expression on its right; otherwise, it returns the value false. Also see operator <= in the index.
+   7. = is the assignment operator, which assigns the value on its right to the variable on its left. Also see operator = in the index.
+   8. == is the “equals” operator, which returns the value true if the expression on its left has the same value as the expression on its right; otherwise, it returns the value false. Also see operator == in the index.
+   9. `>` is the “greater than” operator, which returns the value true if the expression on its left has a greater value than the expression on its right; otherwise, it returns the value false. Also see *operator >* in the index.
+   
+   10. `>=` is the “greater than or equal to” operator, which returns the value true if the expression on its left has the same or a greater value than the expression on its right; otherwise, it returns the value false. Also see *operator >=* in the index.
+   
+   11. `>>` is the “stream input” operator, used to read data from an istream. Also see *operator >>* in the index.
+   
+   12. `[` is the left square bracket; see *square brackets* for usage.
+   
+   13. `]` is the right square bracket; see *square brackets* for usage.
+   
+   14. `[]` is used after the delete operator to tell the compiler that the pointer for which delete was called refers to a group of elements rather than just one data item, *e.g.*, when deleting an array of chars. This is one of the few times when we have to make that distinction explicitly rather than leaving it to context.
+   
+   15. `{` is the left curly brace; see *curly braces* for usage.
+   
+   16. `}` is the right curly brace; see *curly braces* for usage.
+   
+   17. `!=` is the “not equals” operator, which returns the value true if the expression on its left has a value different from the expression on its right; otherwise, it returns the value false. Also see *operator !=* in the index.
+   
+   18. `&&` is the “logical AND” operator. It produces the result true if the expressions on both its right and left are true; if either of those expressions is false, it produces the result false. However, this isn’t the whole story. There is a special rule in C++ governing the execution of the `&&` operator: if the expression on the left is false, then the answer must be false and the expression on the right is not executed at all. The reason for this *short-circuit evaluation rule* is that in some cases you may want to write a right-hand expression that will only be valid if the left-hand expression is true.
+   
+   19. `++` is the increment operator, which adds 1 to the variable to which it is affixed. `+=` is the “add to variable” operator, which adds the value on its right to the variable on its left.
+   
+   20. `-=` is the “subtract from variable” operator, which subtracts the value on its right from the variable on its left.
+   
+   21. `//` is the comment operator; see *comment* for usage.
+   
+   22. `||` is the “logical OR” operator. It produces the result true if at least one of the two expressions on its right and left is true; if both expressions are false, it produces the result false. However, there is a special rule in C++ governing the execution of the `||` operator: if the expression on the left is true, then the answer must be true and the expression on the right is not executed at all. The reason for this *short-circuit evaluation rule* is that in some cases you may want to write a right-hand expression that will only be valid if the left-hand expression is false.
+   
+   23. A `#define` statement is a *preprocessor directive* that defines a *preprocessor symbol*. While this statement can be used to define constant values for general use, it has been mostly superseded except as part of the *include guard* mechanism.
+   
+   24. An `#endif` statement is a *preprocessor directive* that terminates a section of conditional code. It is used in this book as part of the *include guard* mechanism.

25. An **#ifdef** statement is a *preprocessor directive* that begins a section of conditional code. It has the opposite effect from the #ifndef directive.

26. An **#ifndef** statement is a *preprocessor directive* that tells the preprocessor to check whether a particular *preprocessor symbol* has been defined. If not, the following source code is treated normally. However, if the specified preprocessor symbol has been defined, the following source code is skipped by the rest of the compiler as though it were not present in the source file. The #ifndef statement is used in this book as part of the *include guard* mechanism.

27. An **#include** statement is a *preprocessor directive* that has the same effect as that of copying all of the code from a specified file into another file at the point where the #include statement is written. For example, if we wanted to use definitions contained in a file called xstream.h in the implementation file test.cpp, we could insert the include statement #include "xstream.h" in test.cpp rather than physically copying the lines from the file xstream.h into test.cpp.

28. An **access specifier** controls the access of nonmember functions to the member functions and variables of a class. The C++ access specifiers are public, private, and protected. See *public, private,* and *protected* for details. Also see *friend*.

29. **Access time** is a measure of how long it takes to retrieve data from a storage device, such as a hard disk or RAM.

30. An **algorithm** is a set of precisely defined steps guaranteed to arrive at an answer to a problem or set of problems. As this implies, a set of steps that might never end is not an algorithm in the strictest sense.

31. **Aliasing** is the practice of referring to one object by more than one "name"; in C++, these names are actually *pointers* or *references*.

32. The **aliasing problem** is a name for the difficulties that are caused by altering a shared object.

33. An **application program** is a program that actually accomplishes some useful or interesting task. Examples include inventory control, payroll, and games.

34. An **application programmer** (or *class user*) is a programmer who uses native and class variables to write an application program. Also see *library designer*.

35. An **argument** is a value supplied by one function (the *calling function*) that wishes to make use of the services of another function (the *called function*). There are two main types of arguments : *value arguments*, which are copies of the values from the calling function, and *reference arguments*, which are not copies but actually refer to variables in the calling function.

36. An **argument list** is a set of argument definitions specified in a function declaration. The argument list describes the types and names of all the variables the function receives when it is called by a calling function.

37. An **array** is a group of elements of the same type - for example, an array of chars. The array name corresponds to the address of the first of these elements; the other elements follow the first one immediately in memory. As with a vector, we can refer to the individual elements by their indexes. Thus, if we have an array of chars called m_Data, m_Data[i] refers to the ith char in the array. Also see *pointer, vector*.

