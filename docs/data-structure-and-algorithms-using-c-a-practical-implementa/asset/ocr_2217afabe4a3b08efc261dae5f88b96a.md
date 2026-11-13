```
}
int demo :: x=5;
void main()
{
demo obj;
demo :: print();
obj.print();
}
```

OUTPUT 6 7

# 4.11 Constructor and Destructor

# 4.11.1 Constructor

The constructors are the special member functions which are used for the initialization. It is special because it is working and way of representing is totally different from the normal functions. We cannot initialize the data members inside the private section and generally we arrange the data members inside the private section. So if we want to initialize the member than we have to do this inside a member function, which is not preferable because to have an initialized value we have to call a member function. So it will be better to initialize the data members whenever the class members will gets activated for use i.e. when the objects is being created. To achieve the C++ provides the constructors for its conventional programmers.

The constructors are the special member functions which are called automatically whenever an object is being created.

Certain rules we have to follow which using the constructor such as

+   - The name of the constructor is same as the class name.
+   - The constructors do not have any return type not even void.
+   - They cannot be inherited.
+   - The keywords like virtual, const, volatile, static cannot be used.

The constructors are of four types such as

+   - Empty Constructors
+   - Default constructors
+   - Parameterized Constructors
+   - Copy constructors