
```cpp
    5 int main() {
    6    const std::string s{"airplane"};
    7    std::cout << s.substr(3, 4) << '\n'; // retrieve substring "plan"
    8 }
```

```text
plan
```

**Fig. 8.3** | Demonstrating string member function substr. (Part 2 of 2.)

### Checkpoint

- 1. *(Code)* Use `std::string`'s member function `substr` to get a new string containing the three characters from the beginning of `my_string`.  
  Answer: `std::string sub{my_string.substr(0, 3)};`

## 8.5 Swapping strings

`std::string`'s `swap` member function for swapping the contents of two strings. Figure 8.4 swaps the values of `s1` and `s2`, which are not required to have the same length.

```cpp
    1 // Fig08_04.cpp
    2 // Using the swap function to swap two strings.
    3 #include <format>
    4 #include <iostream>
    5 #include <string>
    6
    7 int main() {
    8    std::string s1{"one"};
    9    std::string s2{"two"};
    10
    11   std::cout << std::format("Before swap:\ns1: {}; s2: {}\n\n", s1, s2);
    12   s1.swap(s2); // swap strings
    13   std::cout << std::format("After swap:\ns1: {}; s2: {}\n", s1, s2);
    14 }
```

```text
Before swap:
s1: one; s2: two

After swap:
s1: two; s2: one
```

**Fig. 8.4** | Using the swap function to swap two strings.

### Checkpoint

- 1. *(Code)* Write a statement that swaps the contents of the strings `name1` and `name2`.  
  Answer: `name1.swap(name2);`

## 8.6 string Characteristics

std::string provides member functions for gathering information about a string’s size, capacity, maximum length and other characteristics:

- A string’s size is the number of characters currently stored in the string.
- A string’s capacity is the number of characters that can be stored in the string before it must allocate more memory to store additional characters. A string performs memory allocation for you behind the scenes. The capacity of a string is always at least the string’s current size, though it can be greater. The exact capacity depends on the implementation.
- The maximum size is the largest possible size a string can have. If this value is exceeded, a length_error exception is thrown. In practice, the maximum size is so large in most implementations that you will not encounter this exception.

Figure 8.5 demonstrates string member functions for determining these characteristics. We broke the example into parts for discussion. Function printStatistics (lines 8–12) receives a string and displays its capacity (using member function capacity), maximum size (using member function max_size), size (using member function size) and whether the string is empty (using member function empty).

```cpp
// fig08_05.cpp
// Printing string characteristics.
#include <format>
#include <iostream>
#include <string>

// display string statistics
void printStatistics(const std::string& s) {
    std::cout << std::format(
        "capacity: {}\nmax size: {}\nsize: {}\nempty: {}\n",
        s.capacity(), s.max_size(), s.size(), s.empty());
}
```

**Fig. 8.5** | Printing string characteristics.

The program declares empty string string1 (line 15) and passes it to function printStatistics (line 18). This call to printStatistics indicates that string1’s initial size is 0—it contains no characters. The maximum sizes of strings are larger than you’ll typically need. Object string1 is an empty string, so function empty returns true.

```cpp
int main() {
    std::string string1; // empty string

    std::cout << "Statistics before input:\n";
    printStatistics(string1);
}
```

```text
Statistics before input:
capacity: 15
max size: 9223372036854775807
size: 0
empty: true
```

Line 21 inputs a string (we typed tomato). Line 24 calls printStatistics to output updated string1 statistics. The size is now 6, and string1 is no longer empty.

```cpp
20    std::cout << "\n\nEnter a string: ";
21    std::cin >> string1; // delimited by whitespace
22    std::cout << std::format("The string entered was: {}\n", string1);
23    std::cout << "Statistics after input:\n";
24    printStatistics(string1);
```

```text
Enter a string: tomato
The string entered was: tomato
Statistics after input:
capacity: 15
max size: 9223372036854775807
size: 6
empty: false
```

Line 27 inputs another string (we typed soup) and stores it in string1, replacing "tomato". Line 30 calls printStatistics to output updated string1 statistics. Note that the length is now 4.

```cpp
26    std::cout << "\n\nEnter a string: ";
27    std::cin >> string1; // delimited by whitespace
28    std::cout << std::format("The string entered was: {}\n", string1);
29    std::cout << "Statistics after input:\n";
30    printStatistics(string1);
```

```text
Enter a string: soup
The string entered was: soup
Statistics after input:
capacity: 15
max size: 9223372036854775807
size: 4
empty: false
```

Line 33 uses += to concatenate a 46-character string to string1. Line 36 calls printStatistics to output updated string1 statistics. Because string1’s capacity was not large enough to accommodate the new string size, the capacity was automatically increased to 63 elements, and string1’s size is now 50. How the capacity grows is implementation-defined.

```cpp
// append 46 characters to string1
string1 += "1234567890abcdefghijklmnopqrstuvwxyz1234567890";
std::cout << std::format("\nstring1 is now: {}\n", string1);
std::cout << "Statistics after concatenation:\n";
printStatistics(string1);
```

```text
string1 is now: soup1234567890abcdefghijklmnopqrstuvwxyz1234567890
Statistics after concatenation:
capacity: 63
max size: 9223372036854775807
size: 50
empty: false
```

Line 38 uses the member function `resize` to increase string1’s size by 10 characters. The additional elements are set to null characters. The `printStatistics` output shows that the capacity did not change, but the size is now 60.

```cpp
string1.resize(string1.size() + 10); // add 10 elements to string1
std::cout << "\n\nStatistics after resizing to add 10 characters:\n";
printStatistics(string1);
std::cout << '\n';
}
```

```text
Statistics after resizing to add 10 characters:
capacity: 63
max size: 9223372036854775807
size: 60
empty: false
```

### Checkpoint

- 1. **(Fill-in)** The maximum size of a string is the largest possible size it can have. If this value is exceeded, a(n) ______ exception is thrown. In practice, the maximum size is so large that it’s likely you’ll never encounter this exception.  
  **Answer:** `length_error`.
- 2. **(True/False)** A string’s capacity is the string’s current size.  
  **Answer:** False. Actually, a string’s capacity is always at least the string’s current size, though it can be greater. The exact capacity depends on the implementation.

## 8.7 Finding Substrings and Characters in a string

`std::string` provides member functions for finding substrings and characters in a string. Figure 8.6 demonstrates the find functions. We broke this example into parts for discussion. String s is declared and initialized in line 8.

```cpp
// fig08_06.cpp
// Demonstrating the string find member functions.
#include <format>
#include <iostream>
#include <string>

int main() {
    const std::string s{"noon is 12pm; midnight is not"};
    std::cout << "Original string: " << s;
}
```

```text
Original string: noon is 12pm; midnight is not
```

**Fig. 8.6** | Demonstrating the string find member functions.

### Member Functions find and rfind

Lines 12–13 attempt to find "is" in s using member functions find and rfind, which search from the beginning and end of s, respectively. If "is" is found, the index of the starting location of that string is returned. If the string is not found, the string find-related functions return the constant `std::string::npos` to indicate that a substring or character was not found in the string. The rest of the find functions presented in this section return the same type unless otherwise noted.

```cpp
// find "is" from the beginning and end of s
std::cout << std::format("\n.s.find(\"is\"): {}\n.s.rfind(\"is\"): {}",
    s.find("is"), s.rfind("is"));
```

```text
s.find("is"): 5
s.rfind("is"): 23
```

### Member Function find_first_of

Line 16 uses the member function `find_first_of` to locate the first occurrence in s of any character in "misop". The search is done from the beginning of s. The character 'o' is found at index 1.

```cpp
// find 'o' from beginning
int location{s.find_first_of("misop")};
std::cout << std::format("\n.s.find_first_of(\"misop\") found {} at {}",
    s.at(location), location);
```

```text
s.find_first_of("misop") found o at 1
```

### Member Function find_last_of

Line 21 uses the member function `find_last_of` to find the last occurrence in s of any character in "misop". The searching is done from the end of s. The character 'o' is found at index 27 of the string.
