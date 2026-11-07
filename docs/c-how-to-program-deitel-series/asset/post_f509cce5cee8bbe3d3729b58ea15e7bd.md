
Array class, you’ll indeed understand the essence of object technology—crafting, using and reusing valuable classes.

The chapter concludes with discussions of how you can convert between types (including class types), problems with certain implicit conversions and how to prevent those problems.

## 10.2 Using the Overloaded Operators of Standard Library Class `string`

Figure 10.1 demonstrates many of class string’s overloaded operators and several other useful member functions, including empty, substr and at. Function empty determines whether a string is empty, function substr returns a string that represents a portion of an existing string and function at returns the character at a specific index in a string (after checking that the index is in range). Chapter 21 presents class string in detail.

```cpp
// Fig. 10.1: fig10_01.cpp
// Standard Library string class test program.
#include <iostream>
#include <string>
using namespace std;

int main()
{
   string s1( "happy" );
   string s2( "birthday" );
   string s3;

   // test overloaded equality and relational operators
   cout << "\n\"s1 is \"" << s1 << "\"; s2 is \"" << s2
      << "\"; s3 is \"" << s3 << "\"\n";
   cout << "\n\nThe results of comparing s2 and s1:"
      << "\n s2 == s1 yields " << ( s2 == s1 ? "true" : "false" )
      << "\n s2 != s1 yields " << ( s2 != s1 ? "true" : "false" )
      << "\n s2 > s1 yields " << ( s2 > s1 ? "true" : "false" )
      << "\n s2 < s1 yields " << ( s2 < s1 ? "true" : "false" )
      << "\n s2 >= s1 yields " << ( s2 >= s1 ? "true" : "false" )
      << "\n s2 <= s1 yields " << ( s2 <= s1 ? "true" : "false" );

   // test string member-function empty
   cout << "\nTesting s3.empty():" << endl;

   if ( s3.empty() )
   {
      cout << "s3 is empty; assigning s1 to s3;" << endl;
      s3 = s1; // assign s1 to s3
      cout << "s3 is \"" << s3 << "\"";
   } // end if

   // test overloaded string concatenation operator
   cout << "\n\ns1 += s2 yields s1 = ";

   s1 += s2; // test overloaded concatenation
   cout << s1;

   // test overloaded string concatenation operator with a C string
   cout << "\n\ns1 += \" to you\" yields" << endl;
   s1 += " to you";
   cout << "s1 = " << s1 << "\n\n";

   // test string member function substr
   cout << "The substring of s1 starting at location 0 for\n"
        << "14 characters, s1.substr(0, 14), is:\n"
        << s1.substr( 0, 14 ) << "\n\n";

   // test substr "to-end-of-string" option
   cout << "The substring of s1 starting at\n"
        << "location 15, s1.substr(15), is:\n"
        << s1.substr(15) << endl;

   // test copy constructor
   string s4( s1 );
   cout << "\ns4 = " << s4 << "\n\n";

   // test overloaded copy assignment ( = ) operator with self-assignment
   cout << "assigning s4 to s4" << endl;
   s4 = s4;
   cout << "s4 = " << s4 << endl;

   // test using overloaded subscript operator to create lvalue
   s1[ 0 ] = 'H';
   s1[ 6 ] = 'B';
   cout << "\ns1 after s1[0] = 'H' and s1[6] = 'B' is: "
        << s1 << "\n\n";

   // test subscript out of range with string member function "at"
   try
   {
       cout << "Attempt to assign 'd' to s1.at( 30 ) yields:" << endl;
       s1.at( 30 ) = 'd'; // ERROR: subscript out of range
   } // end try
   catch ( out_of_range &ex )
   {
       cout << "An exception occurred: " << ex.what() << endl;
   } // end catch
} // end main
```

**Fig. 10.1** | Standard Library string class test program. (Part 1 of 3.)

```text
s1 is "happy"; s2 is "birthday"; s3 is ""

The results of comparing s2 and s1:
s2 == s1 yields false
s2 != s1 yields true
s2 > s1 yields false
s2 < s1 yields true
s2 >= s1 yields false
s2 <= s1 yields true

Testing s3.empty():
s3 is empty; assigning s1 to s3;
s3 is "happy"

s1 += s2 yields s1 = happy birthday

s1 += " to you" yields
s1 = happy birthday to you

The substring of s1 starting at location 0 for
14 characters, s1.substr(0, 14), is:
happy birthday

The substring of s1 starting at
location 15, s1.substr(15), is:
to you

s4 = happy birthday to you

assigning s4 to s4
s4 = happy birthday to you

s1 after s1[0] = 'H' and s1[6] = 'B' is: Happy Birthday to you

Attempt to assign 'd' to s1.at( 30 ) yields:
An exception occurred: invalid string position
```

**Fig. 10.1** | Standard Library string class test program. (Part 2 of 3.)

**Fig. 10.1** | Standard Library string class test program. (Part 3 of 3.)

Lines 9–11 create three string objects—s1 is initialized with the literal "happy", s2 is initialized with the literal "birthday" and s3 uses the default string constructor to create an empty string. Lines 14–15 output these three objects, using cout and operator <<, which the string class designers overloaded to handle string objects. Then lines 16–22 show the results of comparing s2 to s1 by using class string’s overloaded equality and relational operators, which perform lexicographical comparisons (i.e., like a dictionary ordering) using the numerical values of the characters (see Appendix B, ASCII Character Set) in each string.

Class string provides member function **empty** to determine whether a string is empty, which we demonstrate in line 27. Member function empty returns true if the string is empty; otherwise, it returns false.

Line 30 demonstrates class string’s overloaded copy assignment operator by assigning s1 to s3. Line 31 outputs s3 to demonstrate that the assignment worked correctly.

Line 36 demonstrates class string’s overloaded += operator for string concatenation. In this case, the contents of s2 are appended to s1. Then line 37 outputs the resulting string that’s stored in s1. Line 41 demonstrates that a string literal can be appended to a string object by using operator +=. Line 42 displays the result.

Class string provides member function substr (lines 47 and 52) to return a portion of a string as a string object. The call to substr in line 47 obtains a 14-character substring (specified by the second argument) of s1 starting at position 0 (specified by the first argument). The call to substr in line 52 obtains a substring starting from position 15 of s1. When the second argument is not specified, substr returns the remainder of the string on which it’s called.

Line 55 creates string object s4 and initializes it with a copy of s1. This results in a call to class string’s *copy constructor*. Line 60 uses class string’s overloaded copy assignment (=) operator to demonstrate that it handles self-assignment properly—we’ll see when we build class Array later in the chapter that self-assignment can be dangerous and we’ll show how to deal with the issues.

Lines 64–65 use class string’s overloaded [] operator to create *lvalues* that enable new characters to replace existing characters in s1. Line 67 outputs the new value of s1. *Class string’s overloaded [] operator does not perform any bounds checking. Therefore, you must ensure that operations using standard class string’s overloaded [] operator do not accidentally manipulate elements outside the bounds of the string.* Class string does provide bounds checking in its member function *at*, which throws an exception if its argument is an invalid subscript. If the subscript is valid, function *at* returns the character at the specified location as a modifiable *lvalue* or a nonmodifiable *lvalue* (e.g., a const reference), depending on the context in which the call appears. Line 73 demonstrates a call to function *at* with an invalid subscript; this throws an out_of_range exception.

## 10.3 Fundamentals of Operator Overloading

As you saw in Fig. 10.1, operators provide a concise notation for manipulating string objects. You can use operators with your own user-defined types as well. Although C++ does *not* allow new operators to be created, it does allow most existing operators to be overloaded so that, when they’re used with objects, they have meaning appropriate to those objects.

Operator overloading is *not* automatic—you must write operator-overloading functions to perform the desired operations. An operator is overloaded by writing a non-static member function definition or non-member function definition as you normally would, except that the function name starts with the keyword operator followed by the symbol for the operator being overloaded. For example, the function name operator+ would be used to overload the addition operator (+) for use with objects of a particular class (or enum). When operators are overloaded as member functions, they must be non-static, because *they must be called on an object of the class* and operate on that object.

To use an operator on an object of a class, you must define overloaded operator functions for that class—with three exceptions:

- The *assignment operator (=)* may be used with *most* classes to perform *memberwise assignment* of the data members—each data member is assigned from the assignment’s “source” object (on the right) to the “target” object (on the left). *Memberwise assignment is dangerous for classes with pointer members*, so we’ll explicitly overload the assignment operator for such classes.
- The *address (&) operator* returns a pointer to the object; this operator also can be overloaded.
- The *comma operator* evaluates the expression to its left, then the expression to its right, and returns the value of the latter expression. This operator also can be overloaded.
