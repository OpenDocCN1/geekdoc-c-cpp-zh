# 2. Parameterized Constructors

In a parameterized constructor, we can pass one or more arguments to the member function so as to assign different initialization values to an object as it is created. Keep in mind that to call this type of constructor, we must use the correct order and type of arguments as defined in the constructor’s prototype. The syntax for a parameterized constructor is as follows:

```
class class_name
{  class_name(argument list..)
    { //body
    }
};
```

# Code: Using Parameterized Constructors

```
#include <iostream>
using namespace std;
class Student
{
    public:
    Student(string n)
    {
    std::cout << "\nThis is a parameterized constructor" <<endl;
    std::cout << "\nName is " <<n<<endl;
    }
};
int main() {
    Student s1("Mary");
    return 0;
}
```

# Output:

```
This is a parameterized constructor
Name is Mary
```

# 3. Copy Constructors

A copy constructor helps to create a copy of another object of a class. The copy is created with all the same values for all data members. The syntax for a copy constructor is as follows:

```
class Class_name
{  Class_name(argument list..)
```