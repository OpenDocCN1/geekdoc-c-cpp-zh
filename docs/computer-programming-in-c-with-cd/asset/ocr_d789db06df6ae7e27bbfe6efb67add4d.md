```
```cpp
db d2;
d1.get_data();
d2.get_data1();
d1.convers1();
d2.convers2();
cout<<add(d1,d2);
return 0;
}

Output:

enter the meters:10
enter the centimeters30
enter the feet50
enter the inches12
84.989998
```
```

![](bbox=[0.224, 0.408, 0.268, 0.444])

With the help of a suitable program explain Constructors with dynamic operations in terms of Copy Constructor.

Let’s explore how to declare and use a destructor in a class.

# Declaring and Using Destructors

In C++, you can destroy an object if it is not needed by using destructors. A destructor is another special member function of a class. It is invoked to destroy an object of a class. The destructor function has the same name as that of the class name but is prefixed by a tilde (~) symbol. The tilde symbol distinguishes it from a constructor of the same class. Listing 19 shows how to declare a destructor within a class (you can find this example in the SimpleDestructor.cpp file on the CD in the code\\chapter6 folder):

+   ▸ Listing 19: Declaring a Destructor

```
```cpp
#include<iostream.h>

class NumberInitialization
{
  int x,y;
  public:
  NumberInitialization();  //constructor prototype
  ~NumberInitialization(); //destructor prototype
};
NumberInitialization::NumberInitialization()
{
  cout<<"Default constructor calling"<<endl;
  x=1;
  y=2;
  cout<<"x="<<x<<endl;
```
```