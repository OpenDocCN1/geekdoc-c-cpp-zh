
## 7.4.2.2 The Subscript and size() Operations

Associated with each character in a string is an integer called an index that is 0 for the first character, 1 for the second, and so on. For example, for a string units declared by

```
string units = "Foot Lbs";
```

a sequential container in memory will be associated with units with the elements numbered 0, 1, 2, ..., and the individual characters that make up the string, F, o, o, t, a space, L, b, and s, will be stored in these elements:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_246_0.png)

The subscript operator [] can be used to access individual characters of a string. In our example, units[0] is a variable of type char whose value is 'F', units[1] is a variable of type char whose value is 'o', and so on; in general, an expression of the form string_object[index] accesses the character at the specified index of string_object. For example, the four assignment statements

```
units[0] = 'I';
units[1] = 'n';
units[2] = 'c';
units[3] = 'h';
```

would change the value of units to "Inch Lbs". If we wish to output these first four characters, we can use a for loop that varies the index over the element positions:

```
for (int i = 0; i < 4; i++)
    cout << units[i] << endl;
```

The size of a string can be found by sending it the size() message, which returns the number of characters in that string. For example, units.size() will return the value 7. Note that the index of the last character in a string is always size() - 1 because indices start at zero. Thus, if we want to process the characters in reverse order, we must start at this index as in the following example:

```
for (int i = units.size() - 1; i >= 0; i--)
    cout << units[i] << endl;
```

## 7.4.2.3 Relational Operators

The relational operators <, >, ==, <=, >=, and != have all been defined for the string class and can be used to compare string objects. For each operation, the elements of the string operands are compared character by character until a mismatch occurs or the end of one (or both) of the strings is reached.

To illustrate, consider the declarations

```
string units1 = "Milligrams",
    units2 = "Millimeters";
```

The boolean expression units1 < units2 is true because the first element where these two strings differ is in position 5 and 'g' < 'm' is true. For the same reason, units1 <= units2 and units1 != units2 are true, whereas units1 > units2, units1 >= units2 and units1 == units2 are false.

If units2 were changed to

```
units2 = "MILLIMETERS";
```

however, units1 < units2 would be false because the first element where these two strings differ is in position 1 and 'i' < 'I' is false (because the numeric code for 'i' is 105 and that for 'I' is 73). This would also be the case if units2 were changed to

```
units2 = "Mill Output";
```

because the first element where units1 and units2 differ is in position 4 and 'i' < ' ' is false (because the numeric code for 'i' is 105 and that for a space is 32).

## 7.4.2.4 Other String Operations

The string class provides several other operations. For example, the program in Example 7.1 used find() to locate the periods in an address and substr() to extract substrings that were the blocks in the address. These and several other commonly used string operations are described in the following table. In this table, s, s1, and s2 are of type string; pos and n are nonnegative integers. Several variations of these operations as well as others are described in Appendix D.

### SOME USEFUL STRING FEATURES

| Output: << | out << s outputs the characters of s to ostream out |
| Input: >>, getline() | in >> s inputs characters from istream in into s until a whitespace character is encountered<br>getline(in, s) inputs an entire line from istream in into s |
| Assignment: = | s = s1 assigns the string expression s1 to s |
| Relational Operators: <, >, ==, <=, >=, != | s1 < s2, s1 > s2, s1 == s2, s1 <= s2, s1 >= s2, and s1 != s2 compare strings |
| Subscript: [] | s[i] is the character in position i of s |
| + | s1 + s2 is the string obtained by concatenating s1 with s2 by appending s2 to s1 |
| string::npos | some integer that is either negative or greater than the maximum length of strings—used to signal unsuccessful string operations (e.g., see find()) |

append()

s1.append(s2) appends s2 onto s1 as in s1 + s2

empty()

s.empty() is true if s contains no characters and is false otherwise

erase()

s.erase(pos, n) erases n characters from s, starting at position pos; if n is too large or is omitted, characters are erased to the end of s

find()

s.find(s1, pos) returns the first position pos at which s1 occurs in s or string::npos if s1 is not found

find_first_of()

s.find_first_of(s1, pos) returns the first position ≥ pos of a character in s1 that matches any character in s or string::npos if none is found

insert()

s.insert(pos, s1) inserts the string s1 into s at position pos

length(), size()

s.length() and s.size() return the number of characters in s

replace()

s.replace(pos, n, s1) replaces the substring of s of length n, starting at position pos, with s1; if n is too large, all the characters to the end of s are replaced

substr()

s.substr(pos, n) returns a copy of the substring consisting of n characters from s, starting at position pos; if n is too large or is omitted, characters are copied only to the end of s

## 7.5 THE C++ complex TYPE

Although the complex number system has many important applications, it is perhaps not as familiar as the real number system. Thus, in this section, we review the basic properties of and operations on complex numbers and describe how they are represented and used in C++ programs.

## 7.5.1 Representation of Complex Numbers

Because complex numbers have two parts, a real part and an imaginary part, they can be plotted in a coordinatized plane by taking the horizontal axis to be the real axis and the vertical axis to be the imaginary axis, so that the complex number a + bi can be represented as the point P(a, b) or, alternatively, as the vector OP from the origin to the point P(a, b):

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_248_0.png)

In C++, the type of a complex object is `complex<T>`, where T is one of the real types `float`, `double`, or `long double`. Each of the types `complex<float>`, `complex<double>`, and `complex<long double>` is a class defined in the `complex` library that must be included in any program that uses one of these types.⁵ A complex literal has the form `complex<T>(a, b)`, where a and b are of type T or can be promoted to that type and represent the real part and the imaginary part of the complex number. The following are some examples:

| C++ Representation | Mathematical Representation |
|---|---|
| `complex<double>(-6.283, 17.1)` | -6.283 + 17.1i |
| `complex<double>(1, 1)` | 1 + i |
| `complex<double>(0, 1)` | i |

## 7.5.2 Operations on Complex Numbers

The sum, difference, and product of two complex numbers z = a + bi and w = c + di are defined by:

z + w = (a + c) + (b + d)i

z - w = (a - c) + (b - d)i

z · w = (ac - bd) + (ad + bc)i

z / w = (ac + bd)/(c² + d²) + (bc - ad)/(c² + d²) i (provided c² + d² ≠ 0)

The sum and difference correspond to the sum and difference of the vector representations of z and w.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_249_0.png)

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_249_1.png)

⁵ The complex library actually contains a class template complex<T>, which is a pattern for a class for complex numbers. When T is replaced by one of float, double, or long double, a class for complex numbers whose real and imaginary parts have that type is created.

The product can be represented by a vector whose length is the product of the lengths of the vectors representing z and w and whose angle from the positive x-axis is the sum of the angles for z and w.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_250_0.png)

To see why this geometric representation of the product of two complex numbers is correct, it is helpful to consider the polar representation of complex numbers. To describe this representation, consider a vector OP from the origin to point P, and suppose that r is the length of OP and that θ is the angle from the positive x-axis to OP, so that the polar coordinates of point P are (r, θ):

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_250_1.png)

It is clear from this diagram that the relation between the rectangular coordinates (a, b) of point P and its polar coordinates (r, θ) is

$a = r \cos \theta$

$b = r \sin \theta$

It follows that the complex number represented by OP can be written in the polar form as

$r \cos \theta + i r \sin \theta = r(\cos \theta + i \sin \theta)$
