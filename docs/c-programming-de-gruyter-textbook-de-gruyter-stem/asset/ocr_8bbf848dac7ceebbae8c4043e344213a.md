# 5 Data Sharing and Protecting

Unfortunately, there are errors during the compiling: we must call general function members through object names.

Still, there are methods that can help us achieve our expectations above, that is, static member functions. The so-called static member function is a function member declared by the keyword static. Just like a static data, a static member function belongs to the whole class, is owned by all the objects of the same class, and is shared by all these objects.

As a member function, the access attribute of a static data member is controlled strictly by class. For a public static member function, we can call it through the class name or object name. A general nonstatic member function can only be called through the object name.

Static members access static data and function members of the class directly. To access nonstatic data members, they first have to get the object name through parameter passing, and then access the nonstatic data member through the object name. Let's have a look at the following program segment:

```
class A
{
    public:
        static void f(A a);
    private:
        int x;
};
void A::f(A a)
{
    cout<<x;      //wrong reference of x
    cout<<a.x;   //correct
}
```

We can find out it is inconvenient for static function members to access nonstatic members. Generally, a static function member is primarily used to access static data members in the same class, and to maintain the data shared among objects.

In UML language, a static function member is represented by adding the <<static>> stereotype to function members.

Example 5.5: Class Point with static data and static function members.

In Example 5.4, we use the static private data member countP to count the number of objects in the Point class; now we use a static function member to access countP in this example. The UML diagram of the Point class that the added static function member is as shown in Figure 5.3:

```
#include <iostream>
using namespace std;
class Point      //define class Point
```