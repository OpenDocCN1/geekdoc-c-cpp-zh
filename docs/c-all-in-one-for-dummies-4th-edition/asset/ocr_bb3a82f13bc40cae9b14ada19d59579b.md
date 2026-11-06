# Using Constants

When you're programming, you may sometimes want a certain fixed value that you plan to use throughout the application. For example, you might want a string containing the name of your company, such as "Bob's Fixit Anywhere Anyhoo". And you don't want someone else working on your application to pass this string into a function as a reference and modify it by mistake, turning it into the name of your global competitor, "Jims Fixum Anyhoo Anytime". That could be bad. Or, if you're writing a scientific application, you might want a fixed number, such as pi = 3.1415926 or root2 = 1.4142135.

You can create such constants in C++ by using the const keyword. When you create a constant, it works just like a variable, except that you can't change it later in the application. For example, to declare your company name, you might use

```
```cpp
const string CompanyName = "Bobs Fixit Anywhere Anyhoo";
```
```

Of course, you can always modify this particular string in your code, but later in your code, you can't do something like this:

```
```cpp
CompanyName = CompanyName + ", Inc.";
```
```

The compiler issues an error for that line, complaining that it's a constant and you can't change it.

After you declare the CompanyName constant, you can use it to refer to your company throughout your code. The Constants example in Listing 2-4 shows you how to do this. Note the three constants toward the top called ParkingSpaces, StoreName, and pi. In the rest of the application, you use these just like any other variables — except that you don't try to change them.

**LISTING 2-4:** Using Constants for Permanent Values That Do Not Change

```
```cpp
#include <iostream>

using namespace std;

const int ParkingSpaces = 80;
const string StoreName = "Joe's Food Haven";
const float pi = 3.1415926;

int main() {
    cout << "Important Message" << endl;
```
```