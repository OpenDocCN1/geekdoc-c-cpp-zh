
> **NOTE**
> 
> For the operator + to work with the **string** data type, one of the operands of + must be a **string** variable. For example, the following statements will not work:
> ```cpp
> str1 = "Hello " + "there!"; //illegal
> str2 = "Sunny Day" + '1';     //illegal
> ```

If str1 = "Hello there", the statement:

```cpp
str1[6] = 'T';
```

replaces the character t with the character T. Recall that the position of the first character in a **string** variable is 0. Therefore, because t is the seventh character in str1, its position is 6.

In C++, [] is called the **array subscript operator**.

As illustrated previously, using the array subscript operator together with the position of the character, you can access an individual character within a **string**.

### EXAMPLE 7-13

The following program shows the effect of the preceding statements.

```cpp
//Example string operations

#include <iostream>                 //Line 1
#include <string>                   //Line 2

using namespace std;                //Line 3

int main()                          //Line 4
{                                   //Line 5
    string name = "William Jacob";  //Line 6
    string str1, str2, str3, str4;  //Line 7

    cout << "Line 8: Name = " << name << endl; //Line 8

    str1 = "Hello There";           //Line 9
    cout << "Line 10: str1 = " << str1 << endl; //Line 10

    str2 = str1;                    //Line 11
    cout << "Line 12: str2 = " << str2 << endl; //Line 12

    str1 = "Sunny";                 //Line 13
    str2 = str1 + " Day";           //Line 14
    cout << "Line 15: str2 = " << str2 << endl; //Line 15

    str1 = "Hello";                 //Line 16
    str2 = "There";                 //Line 17
    str3 = str1 + " " + str2;       //Line 18
    cout << "Line 19: str3 = " << str3 << endl; //Line 19

    str3 = str1 + ' ' + str2;
    cout << "Line 21: str3 = " << str3 << endl;

    str1 = str1 + " Mickey";
    cout << "Line 23: str1 = " << str1 << endl;

    str1 = str1 + " ";
    cout << "Line 25: str1[6] = " << str1[6]
         << endl;

    str1[6] = 'T';
    cout << "Line 27: str1 = " << str1 << endl;

    //string input operations
    cout << "Line 28: Enter a string with "
         << " no blanks: ";
    cin >> str1;

    char ch;
    cin.get(ch);        //Read the newline character
    cout << endl;

    cout << "Line 33: The string you entered = "
         << str1 << endl;

    cout << "Line 34: Enter a sentence: ";
    getline(cin, str2);
    cout << endl;

    cout << "Line 37: The sentence is: " << str2
         << endl;

    return 0;
}
```

**Sample Run:** In the following sample run, the user input is shaded.

```
Line 8: Name = William Jacob
Line 10: str1 = Hello There
Line 12: str2 = Hello There
Line 15: str2 = Sunny Day
Line 19: str3 = Hello There
Line 21: str3 = Hello There
Line 23: str1 = Hello Mickey
Line 25: str1[6] = e
Line 27: str1 = Hello There
Line 28: Enter a string with no blanks: Programming

Line 33: The string you entered = Programming
Line 34: Enter a sentence: Testing string operations

Line 37: The sentence is: Testing string operations
```

The preceding output is self-explanatory, and its unraveling is left as an exercise for you.

## Additional `string` Operations

The data type `string` has a data type, `string::size_type`, and a named constant, `string::npos`, defined as follows:

|  |  |
|---|---|
| `string::size_type` | An unsigned integer (data) type |
| `string::npos` | The maximum value of the (data) type `string::size_type`, a number such as `4294967295` on many machines |

The data type `string` contains several other functions for string manipulation. Table 7-1 describes some of these functions. In this table, we assume that `strVar` is a string variable and `str` is a string variable, a string constant, or a character array. (Arrays are discussed in Chapter 8.)

### Table 7-1. Some `string` functions

| Expression | Effect |
|---|---|
| `strVar.at(index)` | Returns the element at the position specified by `index`. |
| `strVar[index]` | Returns the element at the position specified by `index`. |
| `strVar.append(n, ch)` | Appends `n` copies of `ch` to `strVar`, where `ch` is a `char` variable or a `char` constant. |
| `strVar.append(str)` | Appends `str` to `strVar`. |
| `strVar.clear()` | Deletes all the characters in `strVar`. |
| `strVar.compare(str)` | Returns 1 if `strVar > str`; returns 0 if `strVar == str`; returns −1 if `strVar < str`. |
| `strVar.empty()` | Returns `true` if `strVar` is empty; otherwise it returns `false`. |
| `strVar.erase()` | Deletes all the characters in `strVar`. |
| `strVar.erase(pos, n)` | Deletes `n` characters from `strVar` starting at position `pos`. |
| `strVar.find(str)` | Returns the index of the first occurrence of `str` in `strVar`. If `str` is not found, the special value `string::npos` is returned. |
| `strVar.find(str, pos);` | Returns the index of the first occurrence at or after `pos` where `str` is found in `strVar`. |
| `strVar.find_first_of(str, pos)` | Returns the index of the first occurrence of any character of `strVar` in `str`. The search starts at `pos`. |
| `strVar.find_first_not_of(str, pos)` | Returns the index of the first occurrence of any character of `str` not in `strVar`. The search starts at `pos`. |
| `strVar.insert(pos, n, ch);` | Inserts `n` occurrences of the character `ch` at index `pos` into `strVar`; `pos` and `n` are of type `string::size_type`, and `ch` is a character. |
| `strVar.insert(pos, str);` | Inserts all the characters of `str` at index `pos` into `strVar`. |
| `strVar.length()` | Returns a value of type `string::size_type` giving the number of characters in `strVar`. |
| `strVar.replace(pos, n, str);` | Starting at index `pos`, replaces the next `n` characters of `strVar` with all the characters of `str`. If `n` > length of `strVar`, then all the characters until the end of `strVar` are replaced. |
| `strVar.substr(pos, len)` | Returns a string which is a substring of `strVar` starting at `pos`. The length of the substring is at most `len` characters. If `len` is too large, it means “to the end” of the string in `strVar`. |
| `strVar.size()` | Returns a value of type `string::size_type` giving the number of characters in `strVar`. |
| `strVar.swap(str1);` | Swaps the contents of `strVar` and `str1`. `str1` is a string variable. |

Next, we show how some of these functions work.

### EXAMPLE 7-14 (clear, empty, erase, length, and size FUNCTIONS)

Consider the following statements:

```cpp
string firstName = "Elizabeth";
string name = firstName + " Jones";
string str1 = "It is sunny.";
string str2 = "";
string str3 = "computer science";
string str4 = "C++ programming.";
string str5 = firstName + " is taking " + str4;
string::size_type len;
```

Next, we show the effect of clear, empty, erase, length, and size functions.

| Statement | Effect |
|---|---|
| `str3.clear();` | `str3 = "";` |
| `str1.empty();` | Returns `false` |
| `str2.empty();` | Returns `true` |
| `str4.erase(11, 4);` | `str4 = "C++ program.";` |
| `cout << firstName.length() << endl;` | Outputs 9 |
| `cout << name.length() << endl;` | Outputs 15 |
| `cout << str1.length() << endl;` | Outputs 12 |
| `cout << str5.size() << endl;` | Outputs 36 |
| `len = name.length();` | The value of len is 15 |

The following program illustrates the use of the length function.

```cpp
//Example: clear, empty, erase, length, and size functions

#include <iostream>                                      //Line 1
#include <string>                                        //Line 2

using namespace std;                                     //Line 3

int main()                                               //Line 4
{                                                        //Line 5
    string firstName = "Elizabeth";                     //Line 6
    string name = firstName + " Jones";                  //Line 7
    string str1 = "It is sunny.";                        //Line 8
    string str2 = "";                                    //Line 9
    string str3 = "computer science";                    //Line 10
    string str4 = "C++ programming.";                    //Line 11
    string str5 = firstName + " is taking " + str4;      //Line 12
```
