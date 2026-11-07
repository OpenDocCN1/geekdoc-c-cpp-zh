
Program 10.10  Using strcat and strncat (Continued)

```cpp
17  char str3[20] = "abcdefghijk";
18  const char* str4 = "ABCDEFGHIJK";
19  strncat (str3, str4, 4);
20  cout << "str3: " << str3 << endl;
21  return 0;
22 }
```

Run:

```text
str1: This is a string.
str3: abcdefghijkABCD
```

## Tokenizing

One of the common operations on a string is to find tokens embedded in a string. **String tokens** are substrings separated by delimiters (such as whitespace). The library defines the *strtok* function. To find all tokens in a string, we must call the *strtok* function multiple times. When the *strtok* function is called, it performs three specific tasks:

- 1. It searches the string for the first occurrence of a character not in the delimiter set. The search starts from the character pointed to by the first parameter. If a character is found, it sets the pointer *p* to that character. If not found, it does nothing.
- 2. It then searches for the first occurrence of a character in the delimiter set. If the character is found, it changes that character to a null character.
- 3. It returns the pointer set in the first task.

In Figure 10.6, the *strtok* function finds the first character not in the delimiter set and points *p* to that character. It then finds a character in the delimiter set and changes that character to a null character.

![](img/d68f6199646ca63591a6d8419e0ed4ba_476_0.png)

This means a string has been created by `p` that spans from `p` to the null character. In the second and the following calls, the first parameter is the null pointer and the `strtok` function starts its search from the null pointer created in the previous call. When the function reaches the end of the string, `p` is null.

```cpp
char* p = strtok (str, delimiter);        // Tokenizing str using a delimiter
```

The `strtok(...)` function can be used to split a string into tokens using delimiter characters.

## EXAMPLE 10.12

Program 10.11 uses the `strtok(...)` function to split a string into tokens. The program loops to repeatedly call `strtok` until `p` points to a null character (end of original string). Note that the original string is changed in this process, which means it cannot be a constant string.

Note that Program 10.11 handles two other conditions. First, if the string is empty, `p` in line 15 is set to null and the `while` is skipped, which means nothing is printed. Second, if the string is made of only one word, after the only word is printed in line 18 in the first iteration, `p` is pointed to a null character and the loop is terminated.

## Program 10.11 Tokenizing a string

```cpp
 1 /************************************************************************
 2  * The program shows how we can use the strtok function to extract    *
 3  * tokens from a date.                                                *
 4  ************************************************************************/
 5 #include <cstring>
 6 #include <iostream>
 7 using namespace std;
 8 
 9 int main ( )
10 {
11    // Declaration of a sentence and a pointer
12    char str[ ] = "July 15, 2015";
13    char* p;
14    // Use strtok to extract all words
15    p = strtok (str, " ,"); // first call
16    while (p)
17    {
18        cout << p << endl;
19        p = strtok (0, " ,"); // second, third, and fourth calls
20    }
21    return 0;
 }
```

Run:

```text
July
15
2015
```

## Problems with C Strings

Although C strings provide a way to use strings, they are more error prone and not as robust as C++ strings. We therefore recommend C++ strings be used as much as possible. We discuss C++ strings in the next section.

## 10.2 THE C++ STRING CLASS

The C++ library provides a class named *string*, whose objects are normally referred to as C++ string objects as compared to C string arrays of characters. To use the objects and member functions of this class, we must include the header file `<string>` in our program.

The C++ string library defines a class type whereas the C string library defines an array of characters. When working with a C string, we must create an array of characters and apply functions defined in the `<cstring>` library. When using a C++ string, we can construct a string object and apply the predefined member functions in the `<string>` library to it. We strongly recommend using the C++ string as much as possible.

> To use C++ strings, we need the `<string>` header file.

### 10.2.1 General Design Idea

To better understand how the string class works, we must consider general concepts that designers use in designing the string class. The string class has private data members and public member functions. The user calls the public member functions to manipulate string objects. In general, the data members include a pointer to an array of characters. Other data members keep information about the character array. The data members are normally created in stack memory, but the character array itself is allocated in the heap because its size is not defined until run time. While the C++ string can be visualized as a character array, it is not null terminated as we saw in C strings. Figure 10.7 shows the general picture of a C++ string.

> A C++ string is an array of characters, but it is not null terminated.

![](img/d68f6199646ca63591a6d8419e0ed4ba_478_0.png)

- **Notes:**
- 1. A C++ string is not null terminated.
- 2. Size must be less than or equal to capacity.
- 3. The front is at index 0.
- 4. The back is at index (size − 1).

Figure 10.7  General idea behind the C++ string object

Before discussing each of the member functions, we discuss a metadata type and a constant that are used in the library: *size_type* and *npos*. We show them in a different color to emphasize that they are not fundamental data types; they are type definitions created in the library using fundamental types. The *size_type* is an unsigned int. It is defined as unsigned to prevent a negative integer because size must always be positive. It has two purposes: It is the index of the character array, and it contains the count of a set of characters; in both cases, the value cannot be negative. The constant *npos* has the type *size_type*, and its value is set to −1. The *npos* constant is used to show that we have passed the last element in forward movement or the first element in backward movement. In other words, it is an index that does not exist. These two identifiers are defined in the `std::string` namespace. When we use them in our program, we must qualify them with their namespace as shown below:

```cpp
string :: size_type length;
string :: npos;
```

### 10.2.2 C++ String Library

Before we discuss member functions in the library, we give their prototypes (Table 10.2).

**Table 10.2  Selected members of C++ library**

```cpp
// Constructors
string :: string ()
string :: string (size_type count, char c)
string :: string (const char* cstr)
string :: string (const char* cstr, size_type count)

// Destructor
string :: ~string ()

// Copy constructors
string :: string (const string& str)
string :: string (const string& str, size_type index, size_type length = npos)

// Operations related to size and capacity
size_type string :: size () const
size_type string :: max_size () const
void string :: resize (size_type n, char c )
size_type string :: capacity () const
void string :: reserve (size_type n = 0)
bool string :: empty () const

// Input and output
istream& operator>> (istream& in, string& str)
ostream& operator<< (ostream& out, const string& str)
```

*(continued)*

## Table 10.2  Selected members of C++ library (Continued)

```cpp
istream& getline (istream& in, string& str)
istream& getline (istream& in, string& str, char delim)

// Accessing a character given its position
const char& string :: operator[] (size_type pos) const
char& string :: operator[] (size_type pos)
const char& string :: at (size_type pos) const
char& string :: at (size_type pos)

// Accessing a substring given the position of the first character and length
string string :: substr (size_type pos = 0, size_type length = npos) const

// Finding the position of a given character (forward or backward search)
size_type string :: find (char c, size_type index = 0) const
size_type string :: rfind (char c, size_type index = npos) const

// Finding the position of a character in a set (forward or backward search)
size_type string :: find_first_of (const string& temp, size_type pos = 0)
size_type string :: find_last_of (const string& temp, size_type pos = npos)

// Finding the position of a character not in a set (forward or backward search)
size_type string :: find_first_not_of (const string& temp, size_type pos = 0)
size_type string :: find_last_not_of (const string& temp, size_type pos = npos)

// Comparing two strings
int string :: compare (size_type pos1, size_type n1, const string strg2,
                      size_type pos2, size_type n2) const
int string :: compare (size_type pos1, size_type n1,
                      const char* cstr, size_type n2) const

// Logical comparison of two strings (operator can be <, <=, >, >=, ==, !=)
bool string :: operator< (const string strg1, const string strg2)
bool string :: operator> (const string strg1, const char* cstr)
bool string :: operator== (const char* cstr, const string strg1)

// Pushing a character at the end of a string
void string :: push_back (char c)

// Modifying a string using another string (append, insert, replace, and assign)
string& string :: append (const string& temp)
string& string :: insert (size_type pos, const string& temp)
string& string :: replace (size_type pos, size_type n, const string& temp)
string& string :: assign (size_type pos, size_type n, const string& temp)

// Clearing and erasing a string
void string :: clear ()
```
