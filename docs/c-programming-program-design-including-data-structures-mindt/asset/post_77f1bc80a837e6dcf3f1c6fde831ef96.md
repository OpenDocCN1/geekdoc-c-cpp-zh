
returned by the function `length`. This is because the function `length` returns a value of the type `string::size_type`. Without the cast operator, some compilers might give the following warning message:

`conversion from 'size_t' to 'unsigned int', possible loss of data`

## EXAMPLE 7-15 (find FUNCTION)

Suppose `str1` and `str2` are of type string. The following are valid calls to the function `find`:

```cpp
str1.find(str2)
str1.find("the")
str1.find('a')
str1.find(str2 + "xyz")
str1.find(str2 + 'b')
```

Consider the following statements:

```cpp
string sentence = "Outside it is cloudy and warm.";
string str = "cloudy";
string::size_type position;
```

Next, we show the effect of the find function.

| Statement | Effect |
|---|---|
| `cout << sentence.find("is") << endl;` | Outputs 11 |
| `cout << sentence.find('s') << endl;` | Outputs 3 |
| `cout << sentence.find(str) << endl;` | Outputs 14 |
| `cout << sentence.find("the") << endl;` | Outputs the value of `string::npos` |
| `cout << sentence.find('i', 6) << endl;` | Outputs 8 |
| `position = sentence.find("warm");` | Assigns 25 to `position` |

Note that the search is case sensitive. Therefore, the position of o (lowercase o) in the string `sentence` is 16.

The following program evaluates the previous statements.

```cpp
//Example: find function
#include <iostream>                         //Line 1
#include <string>                           //Line 2

using namespace std;                        //Line 3

int main()                                      //Line 4
{                                               //Line 5
    string sentence = "Outside it is cloudy and warm.";  //Line 6
    string str = "cloudy";                      //Line 7

    string::size_type position;                 //Line 8

    cout << "Line 9: sentence = \"" << sentence
         << "\"" << endl;                       //Line 9

    cout << "Line 10: The position of \"is\" in sentence = "
         << static_cast<unsigned int> (sentence.find("is"))
         << endl;                                //Line 10

    cout << "Line 11: The position of 's' in sentence = "
         << static_cast<unsigned int> (sentence.find('s'))
         << endl;                                //Line 11

    cout << "Line 12: The position of \"" << str
         << "\" in sentence = "
         << static_cast<unsigned int> (sentence.find(str))
         << endl;                                //Line 12

    cout << "Line 13: The position of \"the\" in sentence = "
         << static_cast<unsigned int> (sentence.find("the"))
         << endl;                                //Line 13

    cout << "Line 14: The first occurrence of \'i\' in "
         << "sentence \n"
         << " after position 6 = "
         << static_cast<unsigned int> (sentence.find('i', 6))
         << endl;                                //Line 14

    position = sentence.find("warm");            //Line 15
    cout << "Line 16: Position = " << position << endl;      //Line 16

    return 0;                                     //Line 17
}                                               //Line 18
```

### Sample Run:

```text
Line 9: sentence = "Outside it is cloudy and warm."
Line 10: The position of "is" in sentence = 11
Line 11: The position of 's' in sentence = 3
Line 12: The position of "cloudy" in sentence = 14
Line 13: The position of "the" in sentence = 4294967295
Line 14: The first occurrence of 'i' in sentence
    after position 6 = 8
Line 16: Position = 25
```

The output of this program is self-explanatory. The details are left as an exercise for you. Notice that this program uses the static cast operator to output the value returned by the function find. This is because the function find returns a value of the type `string::size_type`. Without the cast operator, some compilers might give the following warning message:

`conversion from 'size_t' to 'unsigned int', possible loss of data`

## EXAMPLE 7-16 (insert AND replace FUNCTIONS)

Suppose that you have the following statements:

```cpp
string firstString = "Cloudy and warm.";
string secondString = "Hello there";
string thirdString = "Henry is in programming I.";
string str1 = "very ";
string str2 = "Lisa";
```

Next, we show the effect of insert and replace functions.

| Statement | Effect |
|---|---|
| `firstString.insert(10, str1);` | `firstString = "Cloudy and very warm."` |
| `secondString.insert(11, 5, '!');` | `secondString = "Hello there!!!!!"` |
| `thirdString.replace(0, 5, str2);` | `thirdString = "Lisa is in programming I."` |

The following program evaluates the previous statements.

```cpp
//Example: insert and replace functions

#include <iostream>                                  //Line 1
#include <string>                                    //Line 2

using namespace std;                                 //Line 3

int main()                                             //Line 4
{                                                      //Line 5
    string firstString = "Cloudy and warm.";          //Line 6
    string secondString = "Hello there";              //Line 7
    string thirdString = "Henry is in programming I."; //Line 8
    string str1 = "very ";                             //Line 9
    string str2 = "Lisa";                              //Line 10

    cout << "Line 11: firstString = " << firstString  //Line 11
         << endl;
    firstString.insert(10, str1);                      //Line 12

    cout << "Line 13: After insert; firstString = "
         << firstString << endl;                  //Line 13

    cout << "Line 14: secondString = " << secondString
         << endl;                                 //Line 14
    secondString.insert(11, 5, '!');              //Line 15
    cout << "Line 16: After insert; secondString = "
         << secondString << endl;                 //Line 16

    cout << "Line 17: thirdString = " << thirdString
         << endl;                                 //Line 17
    thirdString.replace(0, 5, str2);              //Line 18
    cout << "Line 19: After replace, thirdString = "
         << thirdString << endl;                  //Line 19

    return 0;                                     //Line 20
}                                             //Line 21
```

### Sample Run:

```text
Line 11: firstString = Cloudy and warm.
Line 13: After insert; firstString = Cloudy and very warm.
Line 14: secondString = Hello there
Line 16: After insert; secondString = Hello there!!!!!
Line 17: thirdString = Henry is in programming I.
Line 19: After replace, thirdString = Lisa is in programming I.
```

The output of this program is self-explanatory. The details are left as an exercise for you.

## EXAMPLE 7-17 (substr FUNCTION)

Consider the following statements:

```cpp
string sentence;

string str;

sentence = "It is cloudy and warm.";
```

Next, we show the effect of the substr function.

| Statement | Effect |
|---|---|
| `cout << sentence.substr(0, 5) << endl;` | Outputs: It is |
| `cout << sentence.substr(6, 6) << endl;` | Outputs: cloudy |
| `cout << sentence.substr(6, 16) << endl;` | Outputs: cloudy and warm. |
| `cout << sentence.substr(17, 10) << endl;` | Outputs: warm. |
| `cout << sentence.substr(3, 6) << endl;` | Outputs: is clo |
| `str = sentence.substr(0, 8);` | `str = "It is cl"` |
| `str = sentence.substr(2, 10);` | `str = " is cloudy"` |

The following program illustrates how to use the **string** function `substr`.

```cpp
//Example: substr function
#include <iostream>                                      //line 1
#include <string>                                        //line 2

using namespace std;                                     //line 3

int main()                                               //line 4
{
    string sentence;                                     //Line 6
    string str;                                          //Line 7

    sentence = "It is cloudy and warm.";                //Line 8

    cout << "Line 9: substr(0, 5) in \""
         << sentence << "\" = \""
         << sentence.substr(0, 5) << "\"" << endl;       //line 9

    cout << "Line 10: substr(6, 6) in \""
         << sentence << "\" = \""
         << sentence.substr(6, 6) << "\"" << endl;       //line 10

    cout << "Line 11: substr(6, 16) in \""
         << sentence << "\" = " << endl
         << "             " << sentence.substr(6, 16)
         << "\"" << endl;                                //line 11

    cout << "Line 12: substr(17, 10) in \""
         << sentence << "\" = \""
         << sentence.substr(17, 10) << "\"" << endl;      //line 12

    cout << "Line 13: substr(3, 6) in \""
         << sentence << "\" = \""
         << sentence.substr(3, 6) << "\"" << endl;        //line 13

    str = sentence.substr(0, 8);                          //line 14
    cout << "Line 15: " << "str = \"" << str
         << "\"" << endl;                                //line 15

    str = sentence.substr(2, 10);                         //line 16
    cout << "Line 17: " << "str = \"" << str
         << "\"" << endl;                                //line 17

    return 0;                                             //line 18
}                                                        //line 19
```

### Sample Run:

```text
Line 9: substr(0, 5) in "It is cloudy and warm." = "It is"
Line 10: substr(6, 6) in "It is cloudy and warm." = "cloudy"
```
