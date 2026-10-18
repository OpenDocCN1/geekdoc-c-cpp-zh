
The following segment of a program reads a line of text from the keyboard and displays it on the screen.

```
char c;
cin.get(c); // read a character
while(c != '\n')
{
    cout.put(c); // display the character on screen
    cin.get(c);
}
```

Program 10.1 illustrates the use of these two character handling functions.

# Program 10.1 Character I/O with get() and put()

```
#include <iostream>
using namespace std;

int main()
{
    int count = 0;
    char c;

    cout << "INPUT TEXT\n";
    cin.get(c);

    while(c != '\n')
    {
        cout.put(c);
        count++;
        cin.get(c);
    }
}
```

[PAGE 430]

```
}
cout << "\nNumber of characters = " << count << "\n";

return 0;

}
```

> **NOTE:** *When we type a line of input, the text is sent to the program as soon as we press the RETURN key. The program then reads one character at a time using the statement **cin.get(c);** and displays it using the statement **cout.put(c);**. The process is terminated when the newline character is encountered.*

# getline() and write() Functions

We can read and display a line of text more efficiently using the line-oriented input/output functions **getline()** and **write()**. The **getline()** function reads a whole line of text that ends with a newline character (transmitted by the RETURN key). This function can be invoked by using the object **cin** as follows:

```
cin.getline (line, size);
```

This function call invokes the function **getline()** which reads character input into the variable line. The reading is terminated as soon as either the newline character '\n' is encountered or size-1 characters are read (whichever occurs first). The newline character

is read but not saved. Instead, it is replaced by the null character.

For example, consider the following code:

```
char name[20];
cin.getline(name, 20);
```

Assume that we have given the following input through the keyboard:

Bjarne Stroustrup <press RETURN>

This input will be read correctly and assigned to the character array **name**. Let us suppose the input is as follows:

Object Oriented Programming <press RETURN >

In this case, the input will be terminated after reading the following 19 characters:

Object Oriented Pro

Remember, the two blank spaces contained in the string are also taken into account.

We can also read strings using the operator >> as follows:

```
cin >> name;
```

But remember **cin** can read strings that do not contain white spaces. This means that **cin** can read just one word and not a series of words such as “Bjarne Stroustrup”. But it can read the following string correctly:

Bjarne_Stroustrup

After reading the string, **cin** automatically adds the terminating null character to the character array.

[PAGE 432]

Program 10.2 demonstrates the use of >> and getline() for reading the strings.

# Program 10.2 Reading Strings with getline()

```
#include <iostream>
using namespace std;

int main()
{
    int size = 20;
    char city[20];

    cout << "Enter city name: \\n";
    cin >> city;
    cout << "City name:" << city << "\\n";

    cout << "Enter city name again: \\n";
    cin.getline(city, size);
    cout << "City name now: " << city << "\\n";

    cout << "Enter another city name: \\n";
    cin.getline(city, size);
    cout << "New city name: " << city << "\\n";

    return 0;
}
```

The output of Program 10.2 would be:

First run
Enter city name:

[PAGE 433]

<!-- no content -->

[PAGE 434]

<!-- no content -->

[PAGE 435]

<!-- no content -->

[PAGE 436]

```
cout.write(string1, 10);
```

displays more characters than what is contained in **string1**.

It is possible to concatenate two strings using the **write()** function. The statement

```
cout.write(string1, m).write(string2, n);
```

is equivalent to the following two statements:

```
cout.write(string1, m);
cout.write(string2, n);
```

# 10.5  Formatted Console I/O Operations

C++ supports a number of features that could be used for formatting the output. These features include:

+   - **ios** class functions and flags.
+   - Manipulators.
+   - User-defined output functions.

The **ios** class contains a large number of member functions that would help us to format the output in a number of ways. The most important ones among them are listed in Table 10.2.

**Table 10.2** *ios format functions*

[PAGE 437]

<!-- no content -->

[PAGE 438]

where wis the field width (number of columns). The output will be printed in a field of wcharacters wide at the right end of the field. The width() function can specify the field width for only one item (the item that follows immediately). After printing one item (as per the specifications) it will revert back to the default. For example, the statements

```
cout.width(5);
cout << 543 << 12 << "\\n";
```

will produce the following output:

![](img/62b7c32e48e4f960a8dc2825a7119fb2_438_0.png)

The value 543 is printed right-justified in the first five columns. The specification width(5) does not retain the setting for printing the number 12. This can be improved as follows:

```
cout.width(5);
cout << 543;
cout.width(5);
cout << 12 << "\\n";
```

This produces the following output:

![](img/62b7c32e48e4f960a8dc2825a7119fb2_438_1.png)

Remember that the field width should be specified for each item separately. C++ never truncates the values and therefore, if the specified field width is smaller than the size of the value to be printed, C++ expands the field to fit the value. Program 10.4 demonstrates how the function width() works.

# Program 10.4 Specifying Field Size with width()

[PAGE 439]

<!-- no content -->

[PAGE 440]

```
return 0;
}
```

The output of Program 10.4 would be:

| ITEMS | COST | TOTAL VALUE |
|---:|---:|---:|
| 10 | 75 | 750 |
| 8 | 100 | 800 |
| 12 | 60 | 720 |
| 15 | 99 | 1485 |

**Grand Total = 3755**

> > **NOTE:** *A field of width two has been used for printing the value of sum and the result is not truncated. A good gesture of C++!*

# **Program 10.5** Precision Setting with precision()

```
#include <iostream>
#include <cmath>

using namespace cout;
int main()
{
    cout << “Precision set to 3 digits \n”;
    cout.precision(3);

    cout.width(10);
    cout << “VALUE”;
    cout.width(15);
    cout << “SQRT_OF_VALUE” << “\n”;

    for(int n=1; n<=5; n++)
    {
        cout.width(8);
        cout << n;
        cout.width(13);
        cout << sqrt(n) << “\n”;
    }
    cout << “\n Precision set to 5 digits \n”;
    cout.precision(5); // precision parameter changed
    cout << “ sqrt(10) = “ << sqrt(10) << “\n\n”;

    cout.precision(0); // precision set to default
    cout << “ sqrt(10) = “ << sqrt(10) << “ (default setting)\n”;
}
```

