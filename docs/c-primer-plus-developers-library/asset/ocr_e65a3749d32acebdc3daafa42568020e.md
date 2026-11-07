input. For example, the following function call reads and discards the next 255 characters or up through the first newline character, whichever comes first:

```
```cpp
cin.ignore(255, '\n');
```
```

The prototype provides defaults of 1 and EOF for the two arguments, and the function return type is istream &:

```
```cpp
istream & ignore(int = 1, int = EOF);
```
```

(The EOF default value causes ignore() to read up to the specified number of characters or until end-of-file, whichever comes first.)

The function returns the invoking object. This lets you concatenate function calls, as in the following:

```
```cpp
cin.ignore(255, '\n').ignore(255, '\n');
```
```

Here the first ignore() method reads and discards one line, and the second call reads and discards the second line. Together the two functions read through two lines. Now check out Listing 17.13.

# Listing 17.13 get_fun.cpp

```
```cpp
// get_fun.cpp -- using get() and getline()
#include <iostream>
const int Limit = 255;

int main()
{
    using std::cout;
    using std::cin;
    using std::endl;

    char input[Limit];

    cout << "Enter a string for getline() processing:\n";
    cin.getline(input, Limit, '#');
    cout << "Here is your input:\n";
    cout << input << "\nDone with phase 1\n";

    char ch;
    cin.get(ch);
    cout << "The next input character is " << ch << endl;

    if (ch != '\n')
        cin.ignore(Limit, '\n');    // discard rest of line

    cout << "Enter a string for get() processing:\n";
    cin.get(input, Limit, '#');
    cout << "Here is your input:\n";
```
```