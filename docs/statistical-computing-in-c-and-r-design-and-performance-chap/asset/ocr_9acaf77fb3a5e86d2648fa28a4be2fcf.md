# MISCELLANEOUS TOPICS

# Listing 3.11 stringEx1.cpp

```
//stringEx1.cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    string s1;
    s1 = "Hi ";n    string s2("y'all");
    s1 += s2;
    cout << s1 + " !" << endl;

    cin >> s1;
    cin.get();

getline(cin, s2);
cout << s1 + " " + s2 + " !" << endl;
return 0;
}
```

Lines 8 and 9 of Listing 3.11 use two different string class using the default class constructor to create objects; the first object s1 is created using the string literal "y'all", words surrounded by quotation marks. i.e., the "empty" string s1 is "filled" using an overloaded version of = operator on line 9. On line 11 of the listing two string objects are concatenated via an overloaded +=. Another string is then appended to s1 (using an overloaded +) the result being written to standard output via an overloaded version of the input insertion operator. The exclamation point added at output is excluded in quotation marks. This raises the question of how to create a string that contains a quotation mark. The answer is to use \\\. For example, string s = "\"" produces a string object with a quotation mark as its "value". To obtain a string that contains \ you must use \\\.

Things become more interesting in line 14 of Listing 3.11. The intent is to read the value of string s1 in standard format and then read a string of input (e.g., several words) using the getline function that becomes available through inclusion of the iostream header. The result from our first attempt at is
The first message was expected. But, upon entering "Hi" and a carriage return from the keyboard, the program simply prints out Hi ! and terminates without executing the last group of commands. What has happened is that the newline "character" that was left by cin, and it returns s2 as a blank string. There are several ways to fix this. One is to use the get method on the istream object cin. As used here in the commented statement on line 15 of the listing, get will simply extract and discard the next character in the input stream. When the comments are removed the outputs

```
$ g++ -Wall stringEx1.cpp -o stringEx1
Hi y'all!
Hi
Hi !
```