
A structure may be declared pretty much anywhere in your code. However, by convention, a structure usually is declared just below the preprocessor directives and above main, in the following code fragment:

```cpp
#include <iostream>
#include <string>
using namespace std;
struct Person {
    string name;
    int height;
};
int main () {
    // code
    return 0;
}
```

You may be wondering: "Wait a minute! He is declaring a structure the same place a global variable would be declared and he taught us not to use global variables unless absolutely necessary.

Don't worry, this is not a case of "Do what I say, not what I do." When we are declaring a structure, we are not declaring a variable. Instead, we are declaring a data type. By declaring the data type globally, we will be able to use that type throughout the program. For example, you can't assign a value to a Person structure more than you can assign a value to an instance. Instead, you need to declare variables of the structure. That issue is discussed next.

# Declaring a Structure Variable

On a Saturday evening, I drove to pick up my teenage daughter. The party was noisy, with perhaps one hundred teenagers, each in programming parlance an instance of a Person structure, with their own name and height. Some had no rings, I won't talk about that. Anyway, I was looking for just one particular person, my daughter. When I went up to the parent hosting the party, I did not ask if they knew a generic Person. Instead, I asked if they knew where I could find a particular person, identifying her specifically.

A generic person is the Person structure that in the previous section I showed you how to declare. Here, each particular person is an instance of the Person structure, and each instance needs to be declared as a Person structure variable.

You declare a variable essentially the same as you declare a variable of a built-in data type. The following code declares a Person variable:

```cpp
Person p1;
```

As with the declaration of a variable of a built-in data type, the declaration of the structure starts with the data type, then a variable name, and closes with a semicolon to indicate to the compiler the end of the statement.

You also can declare multiple Person variables, such as:

```cpp
Person p1, p2, p3;
```

Indeed, for the mob scene at the party where I went to pick up my daughter, we want to declare an array of Person variables:

```cpp
Person p[100];
```

You may declare a structure variable essentially anywhere in your program; the same scope and lifetime rules just the way they do for integer, float, and other types of variables.

# Accessing Structure Member Variables

Declaring a structure variable does not assign values to its member variables. You can access a member variable by the name of a structure variable, a data operator, which looks like a period; and the name of the member variable. The following code assigns the value "Emily Kent" to the name member of the Person variable p1:

```cpp
p1.name = "Emily Kent";
```

Similarly, you could output the value of the member variable using the same syntax:

```cpp
cout << "The name of p1 is " << p1.name;
```

Don't make the beginner's mistake using the name of the structure, rather than the name of the structure variable, as in the following example:

```cpp
Person.name = "Emily Kent"; // won't work!
```

The following program declares a three-element Person array, assigns values to the member variables of each element, and outputs their values:

```cpp
#include <iostream>
#include <string>
using namespace std;
const int MAX = 3;
struct Person {
  string name;
  int height;
};
int main () {
  Person p[MAX];
  for (int x = 0; x < MAX; x++) {
    cout << "Enter person's name: ";
    getline(cin, p[x].name);
    cout << "Enter height in inches: ";
    cin >> p[x].height;
    cin.ignore();
  }
  cout << "Outputting data\n";
  cout << "==================================\n";
  for (int x = 0; x < MAX; x++) {
    cout << "Person #" << x + 1 << " name is ";
    cout << p[x].name << " and height is ";
    cout << p[x].height << endl;
  }
  return 0;
}
```

Some sample input and output code:

Enter person's name: Genghis Khent
Enter height in inches: 78
Enter person's name: Jeff Kent
Enter height in inches: 72
Enter person's name: Dante
Enter height in inches: 65
Outputting data
==================================
Person #1 name is Genghis Khent and height is 78
Person #2 name is Jeff Kent and height is 72
Person #3 name is Dante and height is 65

# Initializing a Structure

There are two ways to initialize a structure. The first way is to use initialization list. The second way is to use constructor.

# Initialization Lists

The following code shows how to initialize with initialization list:

```cpp
Person p1 = {"Emily Kent", 72};
```

This may seem like deja vu, the member variables of the structure are initialized. However, the order of variables in the list is important. For example, some compilers will object if you put the values out of order:

```cpp
Person p1 = {72, "Emily Kent"}; // will not work
```

# Constructors

The name of the constructor is always the same as the name of the structure. Additionally, the constructor has no return value. Indeed, some compilers will object if you put a return value in the function header.

The following code demonstrates the use of a constructor:

```cpp
struct Person {
    string name;
    int height;
    Person(string s, int h) {
        name = s;
        height = h;
    }
};

int main() {
    Person p1("Emily Kent", 72);
    return 0;
}
```
