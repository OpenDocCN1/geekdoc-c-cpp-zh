
```
void SphereInColor::setColor(Color newColor)
{
    sphereColor = newColor;
} // end setColor
```

```
Color SphereInColor::getColor() const
{
    return sphereColor;
} // end getColor
```

Notice how the constructors for the class SphereInColor invoke the base-class constructors Sphere() and Sphere(initialRadius). The derived class needs the initialization of the data members in the base class that the base-class constructors can provide. The derived-class constructors then add initializations that are specific to the derived class.

Here is a function that uses the class SphereInColor:

```
void useSphereInColor()
{
    SphereInColor ball(RED);
    ball.setRadius(5.0);
    cout << "The ball diameter is " << ball.getDiameter();
    ball.setColor(BLUE);
    ...
} // end useSphereInColor
```

An instance of a derived class can invoke public methods of the base class

This function uses the constructor and the method setColor from the derived class SphereInColor. It also uses the methods setRadius and getDiameter that are defined in the base class Sphere.

## A.9 Libraries

One of the advantages of modular programming is that you can implement modules independently of other modules. You might also find it possible for several different programs to use a particular module. As a result, you can build a library of modules that you can include in future programs.

Any library—a C++ standard library or any that you write—has a corresponding header that provides information about the contents of the library. For standard libraries, the header is simply an abstraction that the compiler may map to a filename or handle in a different manner. Thus, when using the standard libraries, you do not see the .h extension that ends the names of our own header files.

You have already seen some standard libraries, such as the one that provides input and output services. To use the modules contained in a library, you use the #include directive with the name of the header associated with the library. For example, you write

```
#include <iostream>
using namespace std;
```

Appendix H provides a list of available headers.

User-defined libraries are typically organized into two files. One file, the header file, contains a definition for each class in the library that is available to your program. This file could also contain, for example, function declarations, constant definitions, typedef statements, enumerations, and other include statements. By convention, the name of a header file associated with a user-defined library ends in .h. The other file—the implementation file—contains definitions of the class methods that the header file declares. Typically, the name of an implementation file ends in .cpp.

The assumption, of course, is that the files are in source form—that is, they need to be compiled. It certainly would be more efficient to compile the method definitions once, independently of any particular program, and then later merge the results of the compilation with any program that you desire. In fact, you should compile the implementation file and then include the header file in source form in your program by using an #include directive such as

```
#include "MyHeader.h"
```

You use double quotes instead of angle brackets to enclose the name of a header file that you have written. The mechanics of incorporating the compiled implementation file into your program are system dependent.

Thus, your program can use previously compiled C++ statements, which are no longer available to you in source form. Maybe you did not even write these statements, just as you did not write the standard C++ functions such as sqrt. That is, you use a library in the same spirit in which you use standard functions. Because the header file indicates what is available to you, you must think of a library in terms of what it can do for you and not how it is implemented. You should think of all of your modules in this way, even if you eventually implement them yourself.

## SUMMARY

- 1. Each comment line in C++ begins with two slashes // and continues until the end of the line.
- 2. A C++ identifier is a sequence of letters, digits, and underscores that must begin with either a letter or an underscore.
- 3. You can use a typedef statement to declare new names for data types. These names are simply synonyms for the data types; they are not new data types.
- 4. You define named constants by using a statement of the form
  `const type identifier = value;`
- 5. Enumeration provides another way to name integer constants and to define an integral data type, as in
  `enum Day {SUN, MON, TUE, WED, THU, FRI, SAT};`
- 6. C++ uses short-circuit evaluation for expressions that contain the logical operators && (and) and || (or). That is, evaluation proceeds from left to right and stops as soon as the value of the entire expression is apparent.
- 7. The output operator << places a value into an output stream, and the input operator >> extracts a value from an input stream. You can imagine that these operators point in the direction of data flow. Thus, in cout << myVar, the operator points away from the variable myVar—data flows from myVar to the stream—whereas in cin >> myVar, the operator points to the variable myVar—data flows from the stream into myVar.
- 8. The general form of a function definition is
  ```
  type name(parameter-declaration-list)
  {
     body
  }
  ```
  A valued function returns a value by using the return statement. Although a void function does not return a value, it can use return to exit.

- 9. When invoking a function, the actual arguments must correspond to the parameters in number, order, and type.

- 10. A function makes local copies of the values of any arguments that are passed by value. Thus, the arguments remain unchanged by the function. Such arguments are, therefore, input arguments. A function does not copy arguments that are passed by reference. Rather, it references the actual argument locations whenever the parameters appear in the function definition. In this way, a function can change the values of the arguments, thus implementing output arguments. However, a function does not copy and cannot change a constant reference argument. If copying an input argument would be expensive, make it a constant reference argument instead of a value argument.

- 11. The general form of the if statement is
  ```
  if (expression)
      statement1
  else
      statement2
  ```
  If expression is true, statement1 executes; otherwise statement2 executes.

- 12. The general form of the switch statement is
  ```
  switch (expression)
  {
      case constant1:
          statement1;
          break;
      ...
      case constantn:
          statementn;
          break;
      default:
          statement
  }
  ```
  The appropriate statement executes according to the value of expression. Typically, break (or sometimes return) follows the statement or statements after each case. Omitting break causes execution to continue to the statement(s) after the next case.

- 13. The general form of the while statement is
  ```
  while (expression)
      statement
  ```
  As long as expression is true, statement executes. Thus, it is possible that statement never executes.

- 14. The general form of the for statement is
  ```
  for (initialize; test; update)
      statement
  ```
  where initialize, test, and update are expressions. Typically, initialize is an assignment expression that occurs only once. Then if test, which is usually a logical expression, is true, statement executes. The expression update executes next, usually incrementing or decrementing a counter. This sequence of events repeats, beginning with the evaluation of test, until test is false.

- 15. The general form of the do statement is
  ```
  do
  statement
  while (expression) ;
  ```
  Here, statement executes until the value of expression is false. Note that statement always executes at least once. Also note the required semicolon.

- 16. An array is a container of items that have the same data type. You can refer to these items by using an index that begins with zero. Arrays are always passed to functions by reference.

- 17. A string is a sequence of characters. You can manipulate the entire string, a substring, or the individual characters.

- 18. You must be careful that an array index does not exceed the size of the array. C++ does not check the range of array indices. Similar comments apply to strings.

- 19. An object encapsulates both data and operations on that data. In C++, objects are instances of a class, which is programmer-defined data type.

- 20. A C++ class contains at least one constructor, which is an initialization method, and a destructor, which is a cleanup method that destroys an object when its lifetime ends.

- 21. If you do not define a constructor for a class, the compiler will generate a default constructor—that is, one without arguments—for you. If you do not define a destructor, the compiler will generate one for you. Chapter 4 describes when you need to write your own destructor.

- 22. Members of a class are private unless you designate them as public. The client of the class—that is, the program that uses the class—cannot use members that are private. However, the implementations of methods can use them. You should make the data members of a class private and provide public methods to access some or all of the data members.

- 23. Because certain classes have applications in many programs, you should take steps to facilitate their use. You can define and implement a class within header and implementation files, which a program can include when it needs to use the class.

- 24. A typical C++ program uses header files that you incorporate by using the #include directive. A header file contains class definitions, function declarations, constant definitions, typedef statements, enumerations, and other #include statements. The program might also require an implementation file of function definitions that have been compiled previously and placed into a library. The operating system locates the required implementation file and combines it with the program in ways that are system dependent.
