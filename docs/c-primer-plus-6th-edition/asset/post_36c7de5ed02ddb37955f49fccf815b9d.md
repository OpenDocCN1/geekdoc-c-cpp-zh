
## Comparison Methods and Functions

```
size_type find_first_not_of(const char* s, size_type pos,
             size_type n) const;
size_type find_first_not_of(const char* s, size_type pos = 0) const;
size_type find_first_not_of(char c, size_type pos = 0) const noexcept;
```

These methods work using the corresponding find_first_not_of() methods, except that they search for the first occurrence of any character not in the substring.

Here's code for finding the location of the first two occurrences of the letters not in "This" in a longer string:

```
string longer("That is a funny hat.");
string shorter("That.");
size_type loc1 = longer.find_first_not_of(shorter);// sets loc1 to 2
size_type loc2 = longer.find_first_not_of("Thatch") // sets loc2 to 4
```

The a in That is the first character that does not appear in This. The first in the longer string is the first character not present in Thatch.

## The find_last_not_of() Family

The find_last_not_of() methods have these prototypes:

```
size_type find_last_not_of(const basic_string& str,
             size_type pos = npos) const noexcept;
size_type find_last_not_of(const char* s, size_type pos,
             size_type n) const;
size_type find_last_not_of(const char* s,
             size_type pos = npos) const;
size_type find_last_not_of(char c, size_type pos = npos) const noexcept;
```

These methods work like the corresponding find_last_not_of() methods, except that they search for the last occurrence of any character not in the substring.

Here's code for finding the location of the last two occurrences of the letters not in "This" in a longer string:

```
string longer("That is a funny hat.");
string shorter("That.");
size_type loc1 = longer.find_last_not_of(shorter);// sets loc1 to 15
size_type loc2 = longer.find_last_not_of(shorter, 10); // sets loc2 to 10
```

The last space in longer is the last character that does not appear in shorter. The f in the longer string is the last character not present in shorter found through position 10.

## Comparison Methods and Functions

The string class offers methods and functions for comparing two strings. First, here are the method prototypes:

```
int compare(const basic_string& str) const noexcept;
```

```
int compare(size_type pos1, size_type n1,
const basic_string& str) const;
int compare(size_type pos1, size_type n1,
const basic_string& str,
size_type pos2, size_type n2) const;
int compare(const char* s) const;
int compare(size_type pos1, size_type n1, const char* s) const;
int compare(size_type pos1, size_type n1,
const char* s, size_type n2 ) const;
```

These methods use a traits::compare() method that is defined for the particular character type used for the string. The first method returns a value less than 0 if the first string precedes the second according to the ordering supplied by traits::compare(). It returns 0 if the two strings are the same, and returns a value greater than 0 if the first string follows the second. If two strings are identical to the shorter of the two, the shorter string precedes the longer.

The following examples compare s1 with s3 and s1 with s2:

```
string s1("*bellflower");
string s2("*bell");
string s3("*cat");
int a13 = s1.compare(s3); // a13 is < 0
int a12 = s1.compare(s2); // a12 is > 0
```

The second method is like the first, except that it uses n1 characters, starting from position pos1 in the first string for the comparison.

The following example compares the first four characters in s1 with s2:

```
string s1("*bellflower");
string s2("*bell");
int a2 = s1.compare(0, 4, s2); // a2 is 0
```

The third method is like the first, except that it uses n1 characters, starting from position pos1 in the first string, and n2 characters, starting from pos2 in the second string, for the comparison. For example, the following compares the out in stout to the out in:

```
string s1("*stout boar");
string s2("*mad about ewe");
int a3 = s1.compare(2, 3, s2, 6); // a3 is 0
```

The fourth method is like the first, except that it uses a character array instead of a string object for the second string.

The fifth and sixth methods are essentially like the third, except that they use a character array instead of a string object for the second string.

## 1264 Appendix F The string Template Class

The non-member comparison functions are overloaded relational operators:

```
operator==()
operator<()
operator<=()
operator>()
operator>=()
operator!=()
```

Each operator is overloaded so that it can compare a string object to a string object, a string object to a C-style string, a C-style string to a string object. These operators are defined in terms of the compare() method, so they provide a notationally more convenient way of making comparisons.

## String Modifiers

The string class provides several methods for modifying strings. Most come with an abundance of overloaded versions that they can be used with string objects, arrays, individual characters, and iterator ranges.

## Methods for Append and Adding

You can append one string to another using the overloaded += operator or using an append() method. All throw a length_error if the result would be longer than the maximum string size. The += operators let you append a string, string array, or an individual character to another string:

```
basic_string& operator+=(const basic_string& str);
basic_string& operator+=(const char* s);
basic_string& operator+=(const char c);
```

The append() methods also let you append a string object, a string array, or an individual character to another string. In addition, they let you append part of a string object by specifying an initial position and a number of characters to append or else by specifying a range. You can append part of a string by specifying how many characters of the string to use. The version for appending a character lets you specify how many instances of that character to copy. Here are the prototypes for the append() methods:

```
basic_string& append(const basic_string& str);
basic_string& append(const basic_string& str, size_type pos, size_type n);
template<class Iterator>
basic_string& append(InputIterator first, InputIterator last);
basic_string& append(const char* s, size_type n);
basic_string& append(size_type n, char c);    // appends n copies of c
void push_back(char c);                                     // appends 1 copy of c
```

Here are a couple examples:

```
string test("The");
test.append("ory"); // test is "Theory"
test.append(3,'!'); // test is "Theory!!!"
```

The operator+ is overloaded to enable concatenation. The overloaded functions do not modify a string; instead, they create a new string that consists of one string appended to a second. The addition functions are not member functions, and they allow you to assign a string object to a string object, a string array to a string array, a string object, a string object to a string array, a character to a string object, and a string object to a character. Here are some examples:

```
string st1("red");
string st2("train");
string st3 = st1 + "uce"; // st3 is "reduce"
string st4 = 't' + st2; // st4 is "train"
string st5 = st1 + st2; // st5 is "redrain"
```

## Basic Assignment Methods

In addition to the basic assignment operator, the string class provides assign() methods, which allow you to assign a whole string or a part of a string or a sequence of characters to a string object. Here are the prototypes for the assign() methods:

```
basic_string& assign(const basic_string& str);
basic_string& assign(basic_string& str) noexcept; // C++11
basic_string& assign(const basic_string& str, size_type pos, size_type n);
basic_string& assign(const char* s, size_type n);
basic_string& assign(const char*);
basic_string& assign(size_type n, char c); // assign n copies of c
template<class InputIterator>
basic_string& assign(InputIterator first, InputIterator last);
basic_string& assign(initializer_list<char> l); // C++11
```

Here are a couple examples:

```
string test;
string stuff("set tubes ducks");
test.assign(stuff, 1, 5); // test is "et tu"
test.assign(6, '#'); // test is "######"
```
