
### Program 2.12 Calculating area and perimeter of a circle (Continued)

```cpp
21  // Outputting the value of radius, perimeter, and area
22  cout << "The radius is: " << radius << endl;
23  cout << "The perimeter is: " << perimeter << endl;
24  cout << "The area is: " << area;
25  return 0;
26 }
```

```text
Run:
Enter the radius of the circle: 10.5
The radius is: 10.5
The perimeter is: 65.9734
The area is: 103.631
```

### 2.4.5 Void Type

The **void type** is a special type that has no value. However, it is useful because it can show the lack of any value. For example, we can use void to show that a function returns no value. The lack of value is the same concept we use in real life when we say a *void check*, which is a check that is used for other purposes but has no value. The void type can be used, for example, to show that a function returns nothing.

### 2.4.6 String Class

The string that we have used so far in this chapter is inherited from the C language. It is a collection of characters ending in a null character. For example, the string "John" can be thought of as a collection of five characters 'J', 'o', 'h', 'n', and '\0', the latter of which defines a null character (terminator). We see this type of string in more details when we discuss arrays (collection of elements) in a future chapter.

C++ defines a new string class that is a user-defined type (see Figure 2.11). The **string class** is defined in the C++ library and is more sophisticated and easier to use because many operations are defined for it. We use the **C++ strings** instead of **C strings** gradually until we discuss this class in full in a future chapter.

To use the C++ string, we must include the header file `<string>` in our program as shown below:

```cpp
#include <string>
```

We declare a variable of type string using the following definition:

```cpp
string name;
```

in which *name* is the name of the variable. An object of class string can also be created using double quotes such as "John". One of the differences between the literal of the C string and the object of the C++ string is that the first is made of five characters; the second only of four characters (no null character is needed in a C++ string). The main difference and the advantage of the **C++ string** will reveal itself as we gradually learn to use operations on the objects of this class.

One of the interesting things that we can do with C++ string is concatenation. We can simply use the addition operator (+) to concatenate two or more strings together, as we see in the next example.

### Example 2.18

In this example we write a simple program (Program 2.13) that uses C++ strings. We declare the first name, last name, and initial of a person and, using concatenation, we print the whole name. This is just a simple example of a string class; the most powerful examples are discussed in future chapters.

### Program 2.13 Using string class

```cpp
/***************************************************************
 * This program prints the full name of a person given the first,
 * the middle, and the last name.
 ***************************************************************/
#include <iostream>
#include <string>             // Need to use the string class
using namespace std;

int main ()
{
    // Defining variables
    string first;
    string initial;
    string last;
    string space = " ";
    string dot = ".";
    string fullName;
    // Input data for first name, initial, and last name
    cout << "Enter the first name: ";
    cin >> first;
    cout << "Enter the initial: ";
    cin >> initial;
    cout << "Enter the last name: ";
    cin >> last;
    // Formation of full name using concatenation operator
    fullName = first + space + initial + dot + space + last;
    // Outputting full name
    cout << "The full name is: " << fullName;
    return 0;
}
```

```text
Run:
Enter the first name: John
Enter the initial: A
Enter the last name: Brown
The full name is: John A. Brown
```

## Key Terms

- ASCII
- backslash
- block comment
- Boolean
- Boolean literal
- built-in data type
- C string
- C++ string
- character type
- character literal
- class
- comment
- constant
- data type
- double
- double quote
- enumerated
- floating-point
- floating-point literal
- fundamental data type
- identifier
- include
- include directive
- integer
- integer data type
- integer literal
- keyword
- line comment
- literal
- new line
- preprocessor
- single quotes
- string class
- token
- value
- variable

## Summary

The C++ language is case-sensitive. We normally divide our programs into lines to improve readability. The header file in a program includes predefined code at the top of the program. Every C++ program needs at least one function named main.

A program in C++ uses variables, which have a name and a type.

The *cin* and *cout* objects we use in a program are closely related to the ideas of variable and value. The *cin* object gets data from a keyboard and stores it in a variable; the *cout* object sends a value to the monitor.

The source code in a C++ program is usually made of two things interleaved with each other: code and comments. The code uses the *tokens* of the C++ language; the comments are words in English. A *token* can be an *identifier*, a *literal*, or a *symbol*.

A program written in the C++ language manipulates data. C++ recognizes different types of data: *built-in (fundamental and compound)* and *user-defined (enumerated and class)*. The fundamental data types are divided into three categories: integer, character, and floating-point type. An *integer* is a number without a fraction. A character data type defines a letter. The *Boolean* data type represents a true or false value. The floating-point type represents a number with a fraction.

The C++ language uses two string types; the first is called C-string; the second is called C++ string.

## Problems

- **PR-1.** Locate the errors (if any) in the following program.

  ```cpp
  #include <iostream>
  using namespace std

  int main ()
  {
      cout << 25;
      cout << first;
      return 0;
  }
  ```

- **PR-2.** Locate the errors (if any) in the following program.

  ```cpp
  #include <iostream>

  int main ()
  {
      cout << 35;
      cout << 45;
      return 0;
  }
  ```

- **PR-3.** Locate the errors (if any) in the following program.

  ```cpp
  #include <iostream>
  using namespace std

  int main ();
  {
      std::cout << 35 << endl;
      std::cout << 45;
  }
  ```

- **PR-4.** Locate the errors (if any) in the following program.

  ```cpp
  #include <iostream>
  using namespace std

  int main ()
  {
      int a = 25;
      a + 30 = a;
      cout << a;
      return 0;
  }
  ```

- **PR-5.** Locate the errors (if any) in the following program.

  ```cpp
  #include <iostream>
  using namespace std;

  int main ()
  {
      string name;
      cout << name;
      return 1;
  }
  ```

```cpp
{
    char y = 32;
    char t = 78;
    char z = y + t;
    cout << z;
    return 0;
}
```

- **PR-11.** What is printed from the following program?

  ```cpp
  #include <iostream>
  using namespace std;

  int main ()
  {
      int x = 12;
      int y = 14;
      int z = x + y;
      cout << z;
      return 0;
  }
  ```

- **PR-12.** What is printed from the following program?

  ```cpp
  #include <iostream>
  using namespace std;

  int main ()
  {
      double x = 12.24;
      double y = 14.32;
      cout << x << " + " << y;
      return 0;
  }
  ```

- **PR-13.** What is printed from the following program?

  ```cpp
  #include <iostream>
  using namespace std;

  int main ()
  {
      char x = 'A';
      char y = 'B';
      cout << x << y;
      return 0;
  }
  ```

- **PR-14.** What is printed from the following program?

  ```cpp
  #include <iostream>
  using namespace std;
  ```
