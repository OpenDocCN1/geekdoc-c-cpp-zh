# 5.6 CONSTRUCTORS WITH ONE PARAMETER

A constructor with a single argument is a special type of constructor because it actually defines two operations instead of one. Program 5.3 illustrates this concept. The class brother has a single data member, a string indicating the brother name. Here, a single-argument constructor is introduced. When a string containing the name of the brother is passed to this, it constructs an object of type brother.

# PROGRAM 5.3 Single-argument constructor

```
//SingleArgCons.cpp
#include <iostream>
#include <string>
using namespace std;

class brother
{
    string Name;
public:
    brother(string BrotherName)
    {
        Name = BrotherName;
    }
};

void main()
{
    int j(5);  /* int j = 5 is its shorthand notation */
    int i = int(5);
    double f(3.4);  /* Equivalent of double f = 3.4 */
    brother FirstBrother = brother("Steve Waugh");
    brother SecondBrother("Mark Waugh");
    brother ThirdBrother("Gilchrist");
    brother FourthBrother = "Ricky Ponting";
}
```

# How the Program Works

This program is very simple to understand. Given a single argument to brother constructor, it constructs an object of type brother.

An interesting point to note is the possible ways to invoke a constructor while defining an object. It should be observed that int i = 5; is understood by the compiler as int i(5); this means that the compiler obtains memory that can hold an int, gives the value 5 to it and then assigns it to I; the statement int i = int(5); is also a case of initialization. The object referred by i is initialized by the temporary object created by the compiler. This temporary object is created earlier with initialization to value 5 from int(5).

It can be observed that the same shorthand notations also work for user-defined objects.

```
brother FirstBrother = brother("Steve Waugh");
(explicit call to brother function; i.e., the constructor)
brother SecondBrother("Mark Waugh");
brother FourthBrother = "Ricky Ponting";
```

Here, the second statement is similar to the third one. In all three cases, the compiler calls the user-defined constructor function (brother function defined in the class here) and constructs