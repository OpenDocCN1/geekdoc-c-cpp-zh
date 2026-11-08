+   1. The virtual functions in a base class must be defined, even though it may not be used.
+   2. Virtual functions cannot be static members.
+   3. Virtual functions should be accessed by using object pointers.
+   4. A virtual function can be a friend of another class.
+   5. The prototypes of the base class version of a virtual function and all the derived class versions must be identical. In case the prototypes are different, the virtual function mechanism is lost.
+   6. We cannot have virtual constructors, but we can have virtual destructors.
+   7. When a base pointer points to the object of a derived class, incrementing or decrementing the base pointer will not make it point to the next object of the derived class. Therefore, we should not use this method to move the pointer to the next object.
+   8. If a virtual function is defined in a base class, it need not be necessarily redefined in the derived class. In such cases, calls will invoke the base version.

In the next section, let’s discuss about pure virtual functions.

# # Pure Virtual Functions

In normal practice, a virtual function is declared in the base class and redefined in the derived classes. In addition, the virtual function inside the base class is rarely used for performing any task, that is, it only serves as a placeholder. Therefore, let’s now introduce the concept of pure virtual functions. A pure virtual function is a virtual function that has no definition within the base class. The following syntax is used to declare a pure virtual function:

```
virtual type functionName (arg-list) = 0;
```

When a virtual function is made pure, every derived class that inherits it must provide its own definition by overriding it. If the derived class fails to override the pure virtual function, the compile raises the compile time error. The actual sign in the definition of pure virtual function has nothing to do with the assignment; the value 0 is not assigned to anything. The syntax only tells the compiler that this function will be pure. Let’s write the following program on pure virtual function:

```
1:/* Virtual Function Example Program 6 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class Base {
6:public:
7:    virtual void show () = 0;          /* Pure Virtual Function */
8:};
9:
10:class Derived1 : public Base {
11:public:
12:    void show ()
13:    {
14:        cout<<"Inside class Derived1"<<endl;
15:    }
16:};
17:
18:class Derived2 : public Base {
19:public:
20:    void show ()
21:    {
22:        cout<<"Inside class Derived2"<<endl;
23:    }
```