
Next, we show the effect of the `substr` function.

| Statement | Effect |
|---|---|
| `cout << sentence.substr(0, 5) << endl;` | Outputs: It is |
| `cout << sentence.substr(6, 6) << endl;` | Outputs: cloudy |
| `cout << sentence.substr(6, 16) << endl;` | Outputs: cloudy and warm. |
| `cout << sentence.substr(17, 10) << endl;` | Outputs: warm. |
| `cout << sentence.substr(3, 6) << endl;` | Outputs: is clo |
| `str = sentence.substr(0, 8);` | `str = "It is cl"` |
| `str = sentence.substr(2, 10);` | `str = " is cloudy"` |

The following program illustrates how to use the string function `substr`.

```cpp
//Example: substr function.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string sentence;                                      //Line 1
    string str;                                            //Line 2

    sentence = "It is cloudy and warm.";                  //Line 3

    cout << "Line 4: substr(0, 5) in \""
         << sentence << "\" = \""
         << sentence.substr(0, 5) << "\"\n" << endl;     //Line 4

    cout << "Line 5: substr(6, 6) in \""
         << sentence << "\" = \""
         << sentence.substr(6, 6) << "\"\n" << endl;     //Line 5

    cout << "Line 6: substr(6, 16) in \""
         << sentence << "\" = " << endl
         << "                 " << sentence.substr(6, 16)
         << "\"" << endl;                                //Line 6

    cout << "Line 7: substr(17, 10) in \""
         << sentence << "\" = \""
         << sentence.substr(17, 10) << "\"" << endl;      //Line 7

    cout << "Line 8: substr(3, 6) in \""
         << sentence << "\" = \""
         << sentence.substr(3, 6) << "\"" << endl;        //Line 8
}
```

a function `pigLatinString` to find the pig Latin form of `str`. The previous discussion translates into the following algorithm:

- 1. Get `str`.
- 2. Find the pig Latin form of `str` by using the function `pigLatinString`.
- 3. Output the pig Latin form of `str`.

Before writing the main algorithm, each of these functions is described in detail.

## Function `isVowel`

This function takes a character as a parameter and returns `true` if the character is a vowel and `false` otherwise. The definition of the function `isVowel` is:

```cpp
bool isVowel(char ch)
{
    switch (ch)
    {
    case 'A':
    case 'E':
    case 'I':
    case 'O':
    case 'U':
    case 'Y':
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
    case 'y':
        return true;
    default:
        return false;
    }
}
```

## Function `rotate`

This function takes a string as a parameter, removes the first character of the string, and places it at the end of the string. This is done by extracting the substring, starting at position 1 (which is the second character) until the end of the string, and then adding the first character of the string. The new string is returned as the value of this function. Essentially, the definition of the function `rotate` is:

```cpp
string rotate(string pStr)
{
    string::size_type len = pStr.length();

    string rStr;

    rStr = pStr.substr(1, len - 1) + pStr[0];

    return rStr;
}
```

## Function `pigLatinString`

This function takes a string, `pStr`, as a parameter and returns the pig Latin form of `pStr`. Suppose `pStr` denotes the string to be converted to its pig Latin form. There are three possible cases: `pStr[0]` is a vowel, `pStr` contains a vowel and the first character of `pStr` is not a vowel, or `pStr` contains no vowels. Suppose that `pStr[0]` is not a vowel. Move the first character of `pStr` to the end of `pStr`. This process is repeated until either the first character of `pStr` has become a vowel or all the characters of `pStr` are checked, in which case `pStr` does not contain any vowels. This discussion translates into the following algorithm:

- 1. If `pStr[0]` is a vowel, add "-way" at the end of `pStr`.
- 2. Suppose `pStr[0]` is not a vowel.
- 3. Move the first character of `pStr` to the end of `pStr`. The second character of `pStr` becomes the first character of `pStr`. Now `pStr` may or may not contain a vowel. We use a `bool` variable, `foundVowel`, which is set to `true` if `pStr` contains a vowel and `false` otherwise.
  - a. Suppose that `len` denotes the length of `pStr`.
  - b. Initialize `foundVowel` to `false`.
  - c. If `pStr[0]` is not a vowel, move `pStr[0]` to the end of `pStr` by calling the function `rotate`.
  - d. Repeat Step c until either the first character of `pStr` becomes a vowel or all the characters of `pStr` have been checked.
- 4. Convert `pStr` into the pig Latin form.
- 5. Return `pStr`.

The definition of the function `pigLatinString` is:

```cpp
string pigLatinString(string pStr)
{
    string::size_type len;

    bool foundVowel;

    string::size_type counter;

    if (isVowel(pStr[0]))                         //Step 1
        pStr = pStr + "-way";
    else                                         //Step 2
    {
        pStr = pStr + '-';
        pStr = rotate(pStr);                     //Step 3

        len = pStr.length();                     //Step 3.a
        foundVowel = false;                      //Step 3.b
        for (counter = 1; counter < len - 1;
             counter++)                 //Step 3.d
            if (isVowel(pStr[0]))
            {
                foundVowel = true;
                break;
            }
            else                              //Step 3.c
                pStr = rotate(pStr);
        if (!foundVowel)                       //Step 4
            pStr = pStr.substr(1, len) + "-way";
        else
            pStr = pStr + "ay";
    }
    return pStr;                          //Step 5
}
```

## MAIN ALGORITHM

- 1. Get the string.
- 2. Call the function `pigLatinString` to find the pig Latin form of the string.
- 3. Output the pig Latin form of the string.

## PROGRAM LISTING

```cpp
/*******************************************************
// Author: D. S. Malik
//
// Program: Pig Latin Strings
// This program reads a string and outputs the pig Latin form
// of the string.
*******************************************************/

#include <iostream>
#include <string>

using namespace std;

bool isVowel(char ch);
string rotate(string pStr);
string pigLatinString(string pStr);

int main()
{
    string str;

    cout << "Enter a string: ";
    cin >> str;

    cout << endl;

    cout << "The pig Latin form of " << str << " is: "
         << pigLatinString(str) << endl;

    return 0;
}

//Place the definitions of the functions isVowel, rotate, and
//pigLatinString as described previously here.
```

**Sample Runs:** In these sample runs, the user input is shaded.

### Sample Run 1

Enter a string: `eye`

The pig Latin form of eye is: eye-way

### Sample Run 2

Enter a string: `There`

The pig Latin form of There is: ere-Thay

### Sample Run 3

Enter a string: `why`

The pig Latin form of why is: y-whay

### Sample Run 4

Enter a string: `123456`

The pig Latin form of 123456 is: 123456-way

## QUICK REVIEW

- 1. An enumeration type is a set of ordered values.
- 2. C++’s reserved word `enum` is used to create an enumeration type.
- 3. The syntax of `enum` is:
  
  ```cpp
  enum typeName {value1, value2,...};
  ```
  
  in which value1, value2,... are identifiers, and value1 < value2 < ... .
- 4. No arithmetic operations are allowed on the enumeration type.
- 5. Relational operators can be used with `enum` values.
- 6. Enumeration type values cannot be input or output directly.
- 7. Enumeration types can be passed as parameters to functions either by value or by reference.
- 8. A function can return a value of the enumeration type.
- 9. An anonymous type is one in which a variable’s values are specified without any type name.
- 10. C++’s reserved word `typedef` is used to create synonyms or aliases to previously defined data types.
- 11. Anonymous types cannot be passed as parameters to functions.
- 12. The namespace mechanism is a feature of ANSI/ISO Standard C++.
- 13. A namespace member is usually a named constant, variable, function, or another namespace.
- 14. The scope of a namespace member is local to the namespace.
- 15. One way to access a namespace member outside the namespace is to precede the namespace member name with the namespace name and scope resolution operator.
- 16. In C++, `namespace` is a reserved word.
- 17. To use the namespace mechanism, the program must include the ANSI/ISO Standard C++ header files—that is, the header files without the extension `.h`.
- 18. The using statement simplifies the accessing of namespace members.
- 19. In C++, `using` is a reserved word.
- 20. The keyword `namespace` must appear in the using statement.
- 21. When accessing a namespace member without the using statement, the namespace name and the scope resolution operator must precede the name of the namespace member.
- 22. To use an identifier declared in the standard header files without the namespace name, after including all the necessary header files, the following statement must appear in the program:
  
  ```cpp
  using namespace std;
  ```
  
- 23. A string is a sequence of zero or more characters.
- 24. Strings in C++ are enclosed in double quotation marks.
- 25. To use the type string, the program must include the header file `string`. The other header files used in the program should be ANSI/ISO Standard C++ style header files.
- 26. The assignment operator can be used with the string type.
- 27. The operator + can be used to concatenate two values of the type string. For the operator + to work with the string data type, one of the operands of + must be a string variable.
