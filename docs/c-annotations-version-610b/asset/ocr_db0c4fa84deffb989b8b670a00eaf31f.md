# 5.2.3 Operators

String objects may be manipulated by member functions but also by operators. Using operators often results in more natural-looking code. In cases where operators are available having equivalent functionality as member function the operator is practically always preferred.

The following operators are available for string objects in the examples ‘object’ and ‘argument’ refer to existing `std::string` objects).

+   - **plain assignment:**

a character, C or C++ string may be assigned to a `string` object. The assignment operator returns its left-hand side operand. Example:

```
object = argument;
object = "C string";
object = 'x';
object = 120;       // same as object = 'x'
```

+   - **addition:**

the arithmetic additive assignment operator and the addition operator add text to a string object. The arithmetic assignment operator returns its left-hand side operand, the addition operator returns its result in a temporary string object. When using the addition operator either the left-hand side operand or the right-hand side operand must be a `std::string` object. The other operand may be a char, a C string or a C++ string. Example:

```
object += argument;
object += "hello";
object += 'x';        // integral expressions are OK

argument + otherArgument;    // two std::string objects
argument + "hello";          // using + at least one
"hello" + argument;          // std::string is required
argument + 'a'               // integral expressions are OK
'a' + argument;
```

+   - **index operator:**

The index operator may be used to retrieve object’s individual characters, or to assign new values to individual characters of a non-const string object. There is no range-checking (use the `at()` member function for that). This operator returns a `char &` or `char const &`. Example:

```
object[3] = argument[5];
```

+   - **logical operators:**

the logical comparison operators may be applied to two string objects or to a string object and a C string to compare their contents. These operators return a bool value. The ==, !=, >, >=, and <= operators are available. The ordering operators perform a lexicographical comparison of their contents using the ASCII character collating sequence. Example:

```
object == object;          // true
object != (object + 'x');  // true
object <= (object + 'x');  // true
```

+   - **stream related operators:**

the insertion operator (cf. section 3.1.4) may be used to insert a string object into an ostream, the extraction-operator may be used to extract a string object from an istream. The extraction operator by default first ignores all white space characters