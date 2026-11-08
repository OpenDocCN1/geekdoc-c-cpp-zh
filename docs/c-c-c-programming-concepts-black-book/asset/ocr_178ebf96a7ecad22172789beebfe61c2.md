```
```cpp
friend void show ( exampleOne , exampleTwo );
};

void show (exampleOne obj1, exampleTwo obj2) {
    cout<<"ExampleOne = "<<obj1.memberData<<endl;
    cout<<"ExampleTwo = "<<obj2.memberData<<endl;
}

int main () {
    exampleOne obj1 (10);
    exampleTwo obj2 (55);

    show ();

    return 0;
}
```
```

Output:

```
```
ExampleOne = 10
ExampleTwo = 55
```
```

We have seen in the preceding program the usage of a friend function. Here, we have defined two different classes, namely, exampleOne and exampleTwo, with both having a single data member named “memberData.” In both the functions, we have declared the method show() as a friend function. The friend function is not a part of any of these classes, and since it is defined within the scope for both the classes, the friend function can access the content of these classes, irrespective of where its declaration is made, i.e., in the private or public space of the class definition. Although the preceding example is simple enough, these types of functions are mainly useful while performing operator overloading for both unary and binary operators.

Now that we have understood what friend function is, let us proceed to understand friend class. Friend classes, instead of making a method friend, declare the entire class as a friend. A sample program to demonstrate a friend class is as follows:

```
```cpp
#include <iostream>
using namespace std;

class exampleOne {
    int memberData;
public:
    exampleOne () {
        memberData = 0;
    }
    exampleOne (int var) {
        memberData = var;
    }
    ~exampleOne () {
        memberData = 0;
    }
    friend class exampleTwo;
};

class exampleTwo {
public:
    void show (exampleOne obj) {
        cout <<"From exampleTwo - "<<obj.memberData<<endl;
    }
};
```
```