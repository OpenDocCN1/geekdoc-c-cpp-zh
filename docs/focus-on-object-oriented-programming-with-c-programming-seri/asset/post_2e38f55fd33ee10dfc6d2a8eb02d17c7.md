
## Substring Function

It is often useful to be able to access substrings of String objects. We'll need to extract and return the substring of a String object starting at a particular index in the buffer and of a specified length.

```
String substr(int, int);
```

## Output Function

In order to display the state of any String object, we have to write a print function. This function outputs the literal itself between double quotation marks and outputs the length of the string literal on the same line.

```
void print();
```

It is also useful to overload the operator<<() function to output just the contents of the string pointer itself.

```
friend ostream& operator<<(ostream&, const String&);
```

## Class Inheritance

Inheritance is the process by which a derived class is created as the result of extending, or enhancing, an existing class. Stated differently, the derived class is inherited from a parent (or base) class. This capability saves you from having to "reinvent the wheel", because if a new class greatly resembles an existing class, then all of the properties of the existing class can be inherited into the new class, and any new members can then be added.

Inheritance allows you to collect related classes into a hierarchy with the classes at the top serving as abstractions for those below. This implies that a derived class is a specialization of its parent class. In other words, the derived class is a type of base class, but with more detail added. For this reason, the relationship between a derived class and its base class is called an is-a relationship.

We've seen how a String class could be created and then utilize the capabilities of operator function overloading to make the class interface more intuitive. Now suppose you were to put this class into a library and announce its existence so that users could take advantage of it. But someone then says to you, "The class is fine, except that I meant to overload the unary – as a member function so that it reverses the sequence of letters in the `String` and returns a new instance of the class. What should I do?". Your answer in this case would be for the user to derive a new class from the `String` class and add the new function. Then, when instantiations are made from the newly created class, all of the capabilities of the original class will still be there, plus the added capability of the new function. Since this newly created class is the `String` class with more features, the new class really is a kind of `String` class.

Write a class called `ReverseString` that is publicly derived from the `String` class, with the following member functions:

- a default constructor function
- a copy constructor function
- a constructor function that takes a `const char*` as its one argument
- an overloaded assignment operator
- an overloaded unary `operator~()` function that reverses the letters of the string itself, and returns a new `ReverseString` instance by value (note that the actual contents of the string literal pointed to by `buf` are never modified)

Write a class called `CaseString`, that is publicly derived from the `String` class, with the following data members:

- a pointer, `upper`, of type `char*`, which holds the contents of the string literal in upper case
- a pointer, `lower`, of type `char*`, which holds the contents of the string literal in lower case

Also include the following member functions in the `CaseString` class:

- a default constructor function
- a copy constructor function
- a constructor function that takes a `const char*` as its one argument
- an overloaded assignment operator
- a `print()` function which adds to the output the string literals pointed to by `upper` and `lower`
- a destructor function

Use the `StringDriver` code provided to test your classes.

```cpp
// StringDriver.h
#ifndef _StringDriver_H
#define _StringDriver_H
#include "String.h"
#include "ReverseString.h"
#include "CaseString.h"
int main();
void test1();
void test2();
void test3();
void test4();
void test5();
void test6();
void test7();
void test8();
void test9();
void test10();
void test11();
void test12();
void test13();
void test14();
void test15();
void test16();
void test17();
void test18();
void test19();
void test20();
void wait();
#endif
```

```cpp
// StringDriver.cpp
#include <iostream>
#include <fstream>
#include <stdlib.h>
#include "StringDriver.h"
using namespace std;
ofstream csis;

int main() {
    csis.open("cis.txt");
    test1();
    test2();
    test3();
    test4();
    test5();
    test6();
    test7();
    test8();
    test9();
    test10();
    test11();
    test12();
    test13();
    test14();
    test15();
    test16();
    test17();
    test18();
    test19();
    test20();
    csis.close();
}

void test1() {
    cout << "1. Testing S1: String default constructor."
         << endl << endl;
    csis << "1. Testing S1: String default constructor."
         << endl << endl;
    String s1;
    s1.print();
    wait();
}

void test2() {
    cout << "2. Testing S2: String one arg (char *) constructor."
         << endl << endl;
    csis << "2. Testing S2: String one arg (char *) constructor."
         << endl << endl;
    String s2("ABC");
    s2.print();
    wait();
}

void test3() {
    cout << "3. Testing S3: String one arg (char) constructor,"
         << endl << endl;
    csis << "3. Testing S3: String one arg (char) constructor."
         << endl << endl;
    String s3("Z");
    s3.print();
    wait();
}

void test4() {
    cout << "4. Testing S4: String one arg (int) constructor,"
         << endl << endl;
    csis << "4. Testing S4: String one arg (int) constructor."
         << endl << endl;
    String s4(10);
    s4.print();
    wait();
}

void test5() {
    cout << "5. Testing S5, T5: String copy constructor."
         << endl << endl;
    csis << "5. Testing S5, T5: String copy constructor."
         << endl << endl;
    String s5("Purple Rain");
    s5.print();
    String t5(s5);
    t5.print();
    wait();
}

void test6() {
    cout << "6. Testing S6: String two arg (char, int) constructor,"
         << endl << endl;
    csis << "6. Testing S6: String two arg (char, int) constructor."
         << endl << endl;
    String s6("**", 10);
    s6.print();
    wait();
}

void test7() {
    cout << "7. Testing S7, T7, U7: String assignment."
         << endl;
    csis << "7. Testing S7, T7, U7: String assignment."
         << endl;
    String s7("Sally Ride"), t7, u7;
    t7 = u7 = s7;
    s7.print();
    t7.print();
    u7.print();
    wait();
}

void test8() {
    cout << "8. Testing S8: String assignment."
         << endl;
    csis << "8. Testing S8: String assignment."
         << endl;
    String s8("ABC");
    s8.print();
    wait();
}

void test9() {
    cout << "9. Testing S9: Implicit type conversion."
         << endl;
    csis << "9. Testing S9: Implicit type conversion."
         << endl;
    String s9;
    s9 = "ABC";
    s9.print();
    wait();
}

void test10() {
    cout << "10. Testing S10, T10, U10: String concatenation."
         << endl;
    csis << "10. Testing S10, T10, U10: String concatenation."
         << endl;
    String s10("DEE");
    String t10("HI");
    String u10("ABC" + s10 + "G" + t10 + 'I');
    u10.print();
    String v10('X' + u10);
    v10.print();
    wait();
}

void test11() {
    cout << "11. Testing S11, T11: String concatenation."
         << endl << endl;
    csis << "11. Testing S11, T11: String concatenation."
         << endl << endl;
    String s11("A");
    String t11("BC");
    s11 += s11 += t11 += 'D';
    s11.println();
    t11.print();
    wait();
}

void test12() {
    cout << "12. Testing S12, T12: String unary operator."
         << endl << endl;
    csis << "12. Testing S12, T12: String unary operator."
         << endl << endl;
    String s12("Unary +");
    String t12(+s12);
    s12.print();
    t12.print();
    t12 = +s12;
    s12.print();
    wait();
}

void test13() {
    cout << "13. Testing S13, T13: String comparison operators."
         << endl << endl;
    csis << "13. Testing S13, T13: String comparison operators."
         << endl << endl;
    String s13("ABC"), t13("ABCD");
    s13.print();
    t13.print();
    cout << endl;
    cout << "==" << (s13 == t13 ? "True" : "False") << endl;
    cout << "!=" << (s13 != t13 ? "True" : "False") << endl;
    cout << "<=" << (s13 <= t13 ? "True" : "False") << endl;
    cout << "<" << (s13 < t13 ? "True" : "False") << endl;
    cout << ">=" << (s13 >= t13 ? "True" : "False") << endl;
    cout << ">" << (s13 > t13 ? "True" : "False") << endl;
    cout << endl;
    csis << "==" << (s13 == t13 ? "True" : "False") << endl;
    csis << "!=" << (s13 != t13 ? "True" : "False") << endl;
    csis << "<=" << (s13 <= t13 ? "True" : "False") << endl;
    csis << "<" << (s13 < t13 ? "True" : "False") << endl;
    csis << ">=" << (s13 >= t13 ? "True" : "False") << endl;
    csis << ">" << (s13 > t13 ? "True" : "False") << endl;
    wait();
}
