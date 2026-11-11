```
```
Derived class constructor calling
Main Program started
Function of derived class
Main Program ended
Derived class destructor calling
Base class destructor calling
```
```

In Listing 8, the Base and Derived classes are created, where the Derived class is inherited from the Base class. The Base class has a default constructor, destructor, and the MyFuncB() function and the Derived class has a default constructor, destructor, and the MyFuncD() function. In the main() function, an object, d, of the Derived class is created, which invokes the constructors and destructors of both the Base and Derived classes. In addition, the d object invokes the MyFuncD() function of its own class between the Main Program started and Main Program ended statements.

Now, what will happen when a base class has overloaded constructors and the derived class has just a default constructor? Listing 9 shows that a base class has overloaded constructors while a derived class has a default constructor only (you can find the BaseOverloadedConstructors.cpp file on the CD in the Code\Chapter7 folder):

# ▶ Listing 9: Overloading the Base Class Constructors

```
```cpp
#include<iostream.h>

class Base
{
    public:
        Base()
        {
            cout<<"Base class constructor (no parameter) calling"<<endl;
        }
        Base(int x)
        {
            cout<<"Base class constructor with one parameter calling"<<endl;
            cout<<"Parameter value is : "<<x<<endl;
        }
        ~Base()
        {
            cout<<"Base class destructor calling"<<endl;
        }
        void MyFuncB()
        {
            cout<<"Function of derived class"<<endl;
        }
};

class Derived:public Base
{
    public:
```
```