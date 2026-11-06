
![](img/7b41666e32fdead550ef74cdd9f6ead0_152_0.png)

Figure 14–1 Including the Boost C++ Libraries in a C++ project

## 14.2 The Position of a Character in a String

Let's use the text «Hello World» for the following example. The string consists of 11 characters (including the space character between the two words). The position of each character is shown here.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| H | e | l | l | o | &nbsp; | W | o | r | l | d |

C++ enumerates characters assuming that the first one is at position 0, the second one is at position 1, and so on. Please note that the space between the two words is considered a character as well.

> **Remember!** A space is a character just like any other character. Just because nobody can see it, it doesn't mean it doesn't exist!

## 14.3 Retrieving an Individual Character From a String

C++ allows you to retrieve the individual characters of a string using substring notation. You can use index 0 to access the first character, index 1 to access the second character, and so on. The index of the last character is 1 less than the length of the string. The following C++ program shows an example.

```cpp
#include <iostream>
using namespace std;

int main() {
    string a;

    a = "Hello World";
```

Let's say that user's input is assigned to variable `str`. You can access the fourth letter using `str.at(3)`, the third letter using `str.at(2)`, and so on.

The C++ program is shown here.

**project_14_3_1**

```cpp
#include <iostream>
using namespace std;
int main() {
    string str;

    cout << "Enter a word with four letters: ";
    cin >> str;

    cout << str.at(3) << str.at(2) << str.at(1) << str.at(0);
    return 0;
}
```

## 14.4 Useful String Functions

### Trimming

Trimming is the process of removing whitespace characters from the beginning or the end of a string.

Some of the whitespace characters that are removed with the trimming process are:

- `" "` an ordinary space
- `"\t"` a tab
- `"\n"` a new line (line feed)
- `"\r"` a carriage return

For example, you can trim any spaces that the user mistakenly entered at the end of a string.

The function that you can use to trim a string is

```cpp
trim_copy(subject)
```

This removes any whitespace characters from both the beginning and the end of `subject`. It is defined in the boost library.

**Example**

**project_14_4a**

```cpp
#include <iostream>
#include <boost/algorithm/string.hpp>
using namespace boost::algorithm;
using namespace std;
int main() {
    string a, b;

    a = "        Hello        ";
    b = trim_copy(a);
    cout << b << " Poseidon!" << endl;       //Outputs: Hello Poseidon!
    return 0;
}
```

### String replacement

```cpp
replace_all_copy( subject, search, replace )
```

This searches in `subject` and replaces all occurrences of the `search` string with the `replace` string. It is defined in the boost library.

**Example**

```cpp
// project_14_4b
#include <iostream>
#include <boost/algorithm/string.hpp>
using namespace boost::algorithm;
using namespace std;
int main() {
  string a, b;

  a = "I am newbie in Java. Java rocks!";
  b = replace_all_copy(a, "Java", "C++");

  cout << b << endl;       //Outputs: I am newbie in C++. C++ rocks!
  return 0;
}
```

### Counting the number of characters

```cpp
subject.length()
```

This returns the length of `subject` or, in other words, the number of characters `subject` consists of (including space characters, symbols, numbers, and so on).

**Example**

```cpp
// project_14_4c
#include <iostream>
using namespace std;
int main() {
  string a, b;

  a = "Hello Olympians!";
  cout << a.length() << endl;       //Outputs: 16

  b = "I am newbie in C++";
  cout << b.length() << endl;       //Outputs: 18
  return 0;
}
```

### Finding string position

```cpp
subject.find( search )
```

This finds the numeric position of the first occurrence of `search` in `subject`.

**Example**

```cpp
#include <iostream>
using namespace std;
int main() {
  int i;
  string a;

  a = "I am newbie in C++, C++ rocks!";
  i = a.find("newbie");

  cout << i << endl;    //Outputs: 5
  return 0;
}
```

> **Remember!** The first character is at position 0.

### Converting to lowercase or uppercase

There are two functions that let you convert all letters in a string to lowercase or uppercase.

**To lowercase**

```cpp
to_lower_copy( subject )
```

This returns the `subject`, converted to lowercase. It is defined in the `boost` library.

**Example**

```cpp
#include <iostream>
#include <boost/algorithm/string.hpp>
using namespace boost::algorithm;
using namespace std;
int main() {
  string a, b;

  a = "My Name is JoHN";
  b = to_lower_copy(a);

  cout << b << endl;    //Outputs: my name is john
  return 0;
}
```

**To uppercase**

```cpp
to_upper_copy( subject )
```

This returns the *subject*, converted to uppercase. It is defined in the `boost` library.

**Example**

**project_14_4f**

```cpp
#include <iostream>
#include <boost/algorithm/string.hpp>
using namespace boost::algorithm;
using namespace std;
int main() {
  string a, b;

  a = "My Name is John";
  b = to_upper_copy(a);

  cout << b << endl;      //Outputs: MY NAME IS JOHN
  return 0;
}
```

### Getting part of a string

```cpp
subject.substr( beginIndex [, length] )
```

This returns a portion of *subject*. Specifically, it starts from position *beginIndex* and returns a substring of *length* characters or up to the end of the *subject*, whichever comes first. The argument *length* is optional. If it is omitted, the substring starting from position *beginIndex* until the end of *subject* is returned.

**Example**

**project_14_4g**

```cpp
#include <iostream>
using namespace std;
int main() {
  string a;

  a = "Hello Athena";

  cout << a.substr(6, 3) << endl;       //Outputs: Ath
  cout << a.substr(6, 300) << endl;     //Outputs: Athena
  cout << a.substr(7) << endl;         //Outputs: thena
  return 0;
}
```

### Checking if string is numeric

```cpp
cin.fail()
```

This returns true if the last `cin` statement fails, and false otherwise. Moreover, if you try to read something with the `cin` statement and something goes wrong, you need to clear the error state of `cin`. This is why the `cin.fail()` function is always used in combination with the functions `cin.clear()` and `cin.ignore()`.

**Example**

```cpp
// project_14_4h
#include <iostream>
#include <boost/algorithm/string.hpp>
using namespace boost::algorithm;
using namespace std;

int main() {
    int a;

    cin >> a;                   //Assume that user enters the word "Hello".
    cout << cin.fail() << endl; //Since cin fails, this displays 1 (true)

    //Clear the error state of cin
    cin.clear();
    cin.ignore(100, '\n');

    cin >> a;                   //Assume that user enters an integer.
    cout << cin.fail() << endl; //If cin succeeds, display 0 (false)

    //If the last cin statement succeeds,
    //there is no need to clear its error state

    return 0;
}
```

### Retrieving an individual character

```cpp
subject.at( index )
```

This returns the character located at *subject's* specified *index*. As already mentioned, the string indexes start from zero. The *index* of the last character is 1 less than the length of the string.

**Example**

```cpp
// project_14_4i
#include <iostream>
using namespace std;
int main() {
    string a = "Hello Hermes";

    cout << a.at(0) << endl;    //outputs: H
    cout << a.at(1) << endl;    //outputs: e
    cout << a.at(5) << endl;    //outputs: a space character
    return 0;
}
```

### Exercise 14.4-1 *Switching the Order of Names*

*Write a C++ program that prompts the user to enter in one single string both first and last name. In the end, the program should change the order of the two names.*

**Solution**

This exercise is not the same as the one that you learned in Chapter 8, which swapped the numeric values of two variables. In this exercise, you must split the string and assign each name to a different variable. If you manage to do so, then you can just rejoin them in a different order.

Let's try to understand this exercise using an example. The string that you must split and the position of its individual character is shown here.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| T | o | m | &nbsp; | S | m | i | t | h |

The character that visually separates the first name from the last name is the space character between them. The problem is that this character is not always at position 3. Someone can have a short first name like "Tom" and someone else can have a longer one like "Robert". Thus, you need something that actually finds the position of the space character regardless of the content of the string.

Function `find()` is what you are looking for! If you use it to find the position of the space character in the string "Tom Smith", it returns the value 3. But if you use it to find the space character in another string, such as "Angelina Brown", it returns the value 8 instead.

> **Notice:** The value 3 is not just the position where the space character exists. It also represents the number of characters that the word "Tom" contains! The same applies to the value 8 that is returned for the string "Angelina Brown". It represents both the position where the space character exists and the number of characters that the word "Angelina" contains!

The C++ program for this algorithm is shown here.

```cpp
#include <iostream>
using namespace std;
int main()
{
    string full_name, name1, name2;
    int space_pos;

    cout << "Enter your full name: ";
    getline(cin, full_name);

    //find the position of space character. This is also the number
    //of characters first name contains
```
