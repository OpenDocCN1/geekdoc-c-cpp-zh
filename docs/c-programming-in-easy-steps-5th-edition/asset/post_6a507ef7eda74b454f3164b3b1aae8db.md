
- 10. Save, compile, and run the program to see the output

![](img/bf8dbdfb89042fadbaa73b4160c74bac_72_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_72_1.png)

Use the `=` assignment operator to assign complete strings and the **assign()** function to assign partial strings.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_72_2.png)

Use the **swap()** function wherever possible, rather than creating additional string variables.

## Finding substrings

A string value can be searched to see if it contains a specified “substring” using the **find()** function of the **<string>** library. Its parentheses should specify the substring to seek as its first argument, and the index number of the character at which to start searching as its second argument.

When a search successfully locates the specified substring, the **find()** function returns the index number of the first occurrence of the substring’s first character within the searched string. When the search fails, **find()** returns a value of -1 to indicate failure.

There are several other functions in the **<string>** library that are related to the **find()** function. Two of these are the **find_first_of()** function and the **find_first_not_of()** function. Instead of seeking the first occurrence of a complete **string**, as **find()** does, the **find_first_of()** function seeks the first occurrence of any of the characters in a specified **string**, and **find_first_not_of()** seeks the first occurrence of a character that is not in the specified **string**.

The **find_last_of()** and **find_last_not_of()** functions work in a similar manner — but begin searching at the end of the **string** then move forwards.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_73_0.png)

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```cpp
#include <string>       // Include string support.
#include <iostream>
using namespace std;
```

- 2. Add a main function containing a final return statement, an initialized string variable declaration, and declaring an integer variable to store search results

```cpp
int main()
{
    string text = "I can resist anything but temptation.";
    int num;
    // Add more statements here.
    return 0;
}
```

- 3. In the main function, insert statements to output the start position of a substring within the entire **string** variable

```cpp
num = text.find("resist", 0);
cout << "Position: " << num << endl;
```

- 4. Next, insert a statement to seek a non-existent substring within the entire **string** variable and output the result

```cpp
num = text.find("nonsuch", 0);
cout << "Result: " << num << endl;
```

- 5. Now, insert a statement to output the start position of the first occurrence of any characters of an “If” substring found within the entire **string** variable

```cpp
num = text.find_first_of("If");
cout << "First :" << num << endl;
```

- 6. Insert a statement to report the string position of the first character not within the “If” substring

```cpp
num = text.find_first_not_of("If");
cout << "First not :" << num << endl;
```

- 7. Next, insert a statement to seek the last occurrence of the letter “t” within the **string** variable and output its position

```cpp
num = text.find_last_of("t");
cout << "Last t: " << num << endl;
```

- 8. Now, add a statement to report the string position of the last character within the string variable that is not a “t”

```cpp
num = text.find_last_not_of("t");
cout << "Last not t: " << num << endl;
```

- 9. Save, compile, and run the program to see the search results indicating failure or the positions when located

![](img/bf8dbdfb89042fadbaa73b4160c74bac_74_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_74_1.png)

The searches are case sensitive, so seeking “If” and “if” may produce different results – here, uppercase ‘I’ matches.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_74_2.png)

The first character in a string is at position zero, not at position one.

## Replacing substrings

The **<string>** library contains a number of useful functions to manipulate substrings. A **string** can be inserted into another **string** using the **insert()** function. This requires the index position at which the **string** should be inserted as its first argument, and the **string** value to be inserted as its second argument.

Conversely, a substring can be removed from a **string** using the **erase()** function. This requires the index position at which it should begin erasing as its first argument, and the number of characters to be erased as its second argument.

The **replace()** function neatly combines the **erase()** and **insert()** functions to both remove a substring and insert a replacement. It requires three arguments specifying the position at which it should begin erasing, the number of characters to be erased, and the replacement **string** to be inserted at that position.

A substring can be copied from a **string** using the **substr()** function, stating the index position at which it should begin copying as its first argument, and the number of characters to be copied as its second argument.

The character at any specified position within a **string** can be copied using the **at()** function, which requires the index position as its argument. The final character in a **string** always has an element index number one less than the length of the **string** – because index numbering starts at zero, not one.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_75_0.png)

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```cpp
#include <string>              // Include string support.
#include <iostream>
using namespace std;
```

- 2. Add a main function containing a final **return** statement, an initialized **string** variable declaration, and a statement outputting the **string** variable value

```cpp
int main()
{
    string text = "I do like the seaside";
    cout << "Original: " << text << endl;
    // Add more statements here.
    return 0;
}
```

- 3. In the main function, insert statements to insert a substring into the variable value at index position 10, and to output the modified **string**

```cpp
text.insert(10, "to be beside");
cout << "Inserted: " << text << endl;
```

- 4. Next, insert statements to erase three characters from the modified **string** value starting at index position two, and to output the revised **string**

```cpp
text.erase(2, 3);
cout << "Erased: " << text << endl;
```

- 5. Now, insert statements to remove 25 characters at index position seven, insert a replacement substring, then output the revised **string** again

```cpp
text.replace(7, 25, "strolling by the sea");
cout << "Replaced: " << text << endl;
```

- 6. Finally, insert statements to output nine copied characters at index position seven, and to output the final character in the string

```cpp
cout << "Copied: " << text.substr(7, 9) << endl;
cout << "Last character: " << text.at(text.size() - 1) << endl;
```

Save, compile, and run the program to see the output showing how the string has been manipulated

![](img/bf8dbdfb89042fadbaa73b4160c74bac_76_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_76_1.png)

The **insert()** function can optionally have a third and fourth argument — specifying the position in the substring at which to begin copying, and the number of characters to be copied.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_76_2.png)

The **replace()** function can optionally have a fourth and fifth argument — specifying the position in the substring at which to begin copying, and the number of characters to be copied.
