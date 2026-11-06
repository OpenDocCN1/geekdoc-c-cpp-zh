```
cout << "Enter last name: ";
cin >> last_name;

//Get Random integer between 100 and 999
random_int = 100 + rand() % 900;

cout << to_lower_copy(last_name.substr(0, 4)) << random_int;
return 0;
}
```

> **Notice:** Please note how the function `substr()` is nested within the function `to_lower_copy()`. The result of the inner (nested) function is used as an argument for the outer function. This is a writing style that most programmers prefer to follow because it helps to save a lot of code lines. Of course, if you nest too many functions, no one will be able to understand your code. A nesting of up to four levels is quite acceptable.

# Exercise 14.4-3  *Creating a Random Word*

Write a C++ program that displays a random word consisting of five letters.

# Solution

To create a random word you need a string that contains all 26 letters of the English alphabet. Then you can use the `rand()` function to choose a random letter between position 0 and 25.

The C++ program for this algorithm is shown here.

```
project_14_4_3

#include <iostream>
#include <ctime>
#include <cstdlib>
using namespace std;
int main() {
    string alphabet;

    srand(time(NULL));

    alphabet = "abcdefghijklmnopqrstuvwxyz";

    cout << alphabet.at(rand() % 26) <<
            alphabet.at(rand() % 26) <<
            alphabet.at(rand() % 26) <<
            alphabet.at(rand() % 26) <<
            alphabet.at(rand() % 26);

    return 0;
}
```