
A constructor is a function that bears the same name as the class. It is automatically called when the object of the class is defined.

```
Student()
{
    roll_no = 0;
}
};

Student st1;

/* Defining an object of class Student, notice the use of
class name 'Student' instead of 'class Student' as a type */
```

Here st1.roll_no is initialized to zero automatically when the statement Student st1; gets executed. It is because the function Student() is defined inside the class Student. The function Student() (not the class Student) is called a constructor. The constructor is automatically called when the object is defined. In this case, when we define Student st1; the Student() function is called. The effect of calling that function initializes the roll number to zero. The advantage is that we do not need to explicitly initialize the roll number to zero when we define an object of student. Suppose we define 100 students or an array of students. Each time the constructor function is automatically called, the roll number for all those students is initialized to zero. We will study about constructors and destructors in detail in Chapter 5.

## Operator Overloading

Suppose we have defined a class for complex variables. A complex variable has two parts, a real part and an imaginary part. If we have named the class as complex, then it is possible to define

```
complex c1, c2;
```

Here, complex is the class name and c1 and c2 are variables of the complex type, that is, the objects of the class complex. It is possible to write c1 + c2 as an expression where + will add the real and imaginary values, respectively. By default + adds only built-in types such as int, float, and double. C++ provides the facility to assign a new meaning to + such that it can now also add two complex variables. This facility is known as operator overloading. Here, we have to overload the + operator to have the required effect. (Readers interested in knowing how this is done can see Chapter 6 on operator overloading wherein the program for addition of complex objects is provided.)

The ultimate goal for providing all such facilities is to make user-defined objects to behave as naturally as possible. In C++, user-defined objects can actually behave in a natural way. Just by looking at the use of the user-defined objects, it is almost impossible to differentiate them from the built-in objects. In C, user-defined data types always look different from the built-in ones (the word 'struct', for example, struct Student, struct employee, and so on).

### 1.11.2 Syntactical Differences

There are a number of syntactical differences between C and C++. The major ones derive from the need to provide the class construct and related issues. Almost all C syntax works fine with all C++ compilers. A few syntactical differences are summarized as follows.

#### Comments

The comments in C++ are of two types. The C-like comments (anything enclosed within /* and */) are acceptable and comments that begin with a // are also allowed. When a // is provided somewhere in the line, the rest of the line is ignored. Look at the following code:

```
/* This itself is a C-like comment, whereas the
following is a C++-like comment */
if (a > b) // checking for a greater than b
printf ("a is greater!");
```

The following is an example that shows how C++ comments replace C-like comments:

```
/* This is the first line of comment.
This is the second line of it.
And this is the third! */

// This is the first line of comment.
// This is the second line of it.
// And this is the third!
```

In short, // is useful for a single-line comment, but for multiple lines, one may prefer to use /* and */.

Moreover, // is valid until the end of the line, so it cannot replace a C-like comment used within the following statement:

```
if (a > b)        /* checking for a > b!*/
printf("a is greater!");
```

#### Input/Output Operators

Though printf() is used in the program statements given in Section 1.11.2, it is usually not used in the C++ programs.

```
cout << "a is greater";
```

can do the same job in C++ as printf().

Here, cout is an object of the standard output stream class. It is one of the most useful objects of C++. We have to include <iostream> file for the prototype of iostream (input output stream, to be precise) objects. We can see that iostream is similar to stdio.h used in C. It should be remembered that we still need to use stdio.h for the prototypes of the functions using input and output stream such as printf() and scanf().

If it is possible to use stdout in C++ (i.e., printf(), scanf(), etc.), then why do we need a new way to output? This question is answered in detail in Chapter 12. In summary, the newer approach is better and easier to program. At times, this approach is the only way while providing the input and output of user-defined objects similar to built-in types. For example, it is possible to have a student Lara and then use cout<< Lara to print the details about Lara. We need to overload operator << for the same. This is not possible with printf(). As mentioned earlier, if printf() is used, one needs to include <stdio.h>. The user running the program finds no difference between the output produced by printf() and cout.

While using ANSI C++, one should use <cstdio> and not <stdio.h>. The usage of <cstdio> is similar to the functionality of <stdio.h>, that is, either

While coding the C++ programs, one should use cin for reading rather than scanf() and cout for printing rather than printf(). These constructs are simpler and better.

In the case of compilers that can compile both the C and C++ programs, the file name extension determines the type of code. In TurboC or VC++, '.c' is a C program whereas '.cpp' is a C++ program.

The << operator used by cout and >> used by cin are examples of operator overloading.

<cstdio> or <stdio.h> will provide printf(), scanf(), etc. in exactly the same way. Still, there is a huge difference between them. This difference is explained in Chapter 14. Similarly, there is a difference if we want to use the other C header files (e.g., <math.h> becomes <cmath>).

There is another seemingly minor difference between using the functions such as printf() in C and C++. With most of the C compilers, it is possible to use printf() or scanf() while not including <stdio.h>. Such programs can be compiled and will also work as expected. The inclusion of <stdio.h> does not seem to be necessary (because the stdio.h only contains the prototype of the function). Why is it so? Let us try to understand this.

The compiled code of printf()(and other functions as well) is kept in the library. The library contains the object code for all functions that are a part of the library. The code of printf() and scanf() gets added to the program code after compilation and before the executable code is generated.

Note A C program does not need a prototype to use a function. The C compiler might flag a warning at the most if the prototype of the function is missing. A C++ program, on the contrary, will not compile unless the prototype is available. Prototyping is a must in C++. If we use printf() or scanf() and do not have a header for stdio.h, the program will not compile in C++.

In the case of cout, << is actually an overloaded operator. This means that <<, which is basically a bitwise left shift operator, is given a new meaning here. The process of providing a new additional meaning to an existing operator is known as operator overloading. It should be remembered that we can still use << as a bitwise left shift operator. The new meaning given is an extra one (in addition to the original meaning).

Similarly, we can use >> operator (again, overloaded) for reading purpose. We use an object of standard input stream cin for this purpose. A built-in object of iostream class, cin is used to read an element from the console. So, the following statement can be used to read a string variable, where its name is assumed to be StringVariable:

```
cin >> StringVariable
```

We do not need to provide the data type with cin or cout (such as %d or %s), nor do we need to append an & operator in front of the variable while reading a variable value as in scanf. In C++, cout formats the output in a default way, which is suited for most of the cases. We will learn how to format the data different than the default way in Chapter 12.

#### C++ Headers

We cannot use stdio.h for using cout or cin. We need to write #include <iostream> to use cout and cin in our program. The omission of .h in the name of the header file <iostream> should be noted. This is a new style in ANSI C++. Older C++ programs use a file <iostream.h>. If we write <iostream.h> instead of <iostream>, and it might work with most of the existing C++ compilers. Please understand that it is provided only for backward compatibility. The use of <iostream.h> is no longer recommended in C++.

We will see the difference between using iostream and iostream.h when we learn about namespaces in Chapter 14.

#### Return Types

The return type in C is by default int, whereas in C++, it is not so and hence we must specify it. For example,
