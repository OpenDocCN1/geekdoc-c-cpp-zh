```
const int MAX = 3;
struct Person {
    string name;
    int height;
    Person() {
        name = "No name assigned";
        height = -1;
    }
};
```

```
int main () {
    Person p1;
    cout << "The person's name is " << p1.name << " and height is " << p1.height << endl;
    return 0;
}
```

The output reflects the default values:
The person's name is No name assigned and height is -1

> **Note** This no-argument constructor, like the default, is called by the statement Person p1. Though a no argument constructor is called, there are no empty parentheses following p1 since it is not a function call but instead a variable declaration.

# Constructors with Arguments

Declaring a no-argument constructor is an improvement over the default constructor since the member variables have default values. However, it would be even better if we could truly initialize the member variables with values supplied by the user when the program is running. This is possible if we add arguments to the constructor, each argument being used to initialize a member variable. Accordingly, add the following two-argument constructor to initialize the definition of the Person structure:

```
Person(string s, int h) {
    name = s;
    height = h;
}
```

The program now reads
#include <iostream>
#include <string>
using namespace std;
const int MAX = 3;
struct Person {
    string name;
    int height;
    Person() {
        name = "No name assigned";
        height = -1;
    }