```
getline(cin, s.name); /* We use the getline() function to read characters and store them in name. */
cout << "Code: ";
cin >> s.code;

cout << "Grade: ";
cin >> s.grd;

s.show();
return 0;
}
```

By default, the cin object is associated with the keyboard. Similar to cout and <<, the >> does not perform a shift operation, it is overloaded to get data input from cin. The string class is one of the many available C++ classes and it is used for string manipulation. The important thing to notice is the existence of a function declaration inside the class. Functions declared inside a class are said to be member functions. A member function may be defined inside or outside its class. The first approach is typically used for very short functions. If it is not short, it is usually defined outside the class so that its code is clearly shown, not mixed together with other declarations. Although the code of the function show() is short, we implemented it outside the class to show you how to do it. We use the scope resolution operator :: preceded by the name of the class that it belongs to. show() outputs the values of the members of the calling object.

Let's talk about accessibility. The accessibility defines the access to the class data. It is a feature missing from C. In C, the data of a structure or union are all accessible. We cannot make some of them inaccessible. In C++, the members of a class can be public, private, or protected. There is no restriction in the access of the public members. The private members are accessible by the member functions of the same class. The protected members are like the private members for the same class, but they are accessible from functions in classes derived from this class. By default, the class data are private. The main advantage to restrict access in class data is to secure the code and avoid the case of unwanted modifications. Restricted access is a major feature of object-oriented programming. Let's find the errors in the following program:

```
#include <iostream>
using namespace std;

class Test
{
private: // Not needed.
    int a;
    void f1();
protected:
    int b;
    void f2();
public:
    int c;
    void f3();
};
```