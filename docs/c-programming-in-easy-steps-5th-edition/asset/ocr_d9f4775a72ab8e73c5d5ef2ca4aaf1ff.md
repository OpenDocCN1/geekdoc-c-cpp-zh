# Calling base constructors

Although derived classes inherit the members of their parent base class, they do not inherit its constructor and destructor. However, it should be noted that the default constructor of the base class is always called when a new object of a derived class is created – and the base class destructor is called when the object gets destroyed. These calls are made in addition to those made to the constructor and destructor methods of the derived class.

The default constructor of the base class has no arguments – but that class may also have overloaded constructors which do. If you prefer to call an overloaded constructor of the base class when a new object of a derived class is created, you can create a matching overloaded constructor in the derived class – having the same number and type of arguments.

![](bbox=[0.118, 0.287, 0.188, 0.353])

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.
+   
+   ```cpp
+   #include <iostream>
+   using namespace std ;
+   ```

+   2. Declare a class named “Parent”, which will be a base class.
+   
+   ```cpp
+   class Parent
+   {
+       // Class members go here.
+   } ;
+   ```

+   3. Between the braces of the Parent class declaration, insert a public access specifier and add a default constructor to output text – identifying when it has been called.
+   
+   ```cpp
+   public:
+       Parent()
+       { cout << “Default Parent constructor called.”; }
+   ```

+   4. Add an overloaded constructor, which takes a single integer argument, and also outputs identifying text.
+   
+   ```cpp
+       Parent ( int a )
+       { cout << endl <<
+           “Overloaded Parent constructor called.”; }
+   ```

+   5. After the Parent class, declare a derived “Daughter” class.
+   
+   ```cpp
+   class Daughter : public Parent
+   {
+   
+   };
+   ```

![](bbox=[0.118, 0.72, 0.258, 0.812])

+   6. In the Daughter class declaration, insert a public access specifier and add a default constructor to output text – identifying when it has been called.
+   
+   ```cpp
+   public:
+       Daughter ()
+       { cout << endl <<
+           “Derived Daughter class default constructor called.”; }
+   ```

+   7. After the Daughter class, declare a derived “Son” class.