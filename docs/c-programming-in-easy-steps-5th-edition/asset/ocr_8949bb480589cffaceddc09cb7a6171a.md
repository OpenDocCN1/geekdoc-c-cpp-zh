# Overriding base methods

A method can be declared in a derived class to override a matching method in the base class – if both method declarations have the same name, arguments, and return type. This effectively hides the base class method as it becomes inaccessible unless it is called explicitly, using the :: scope resolution operator for precise identification.

The technique of overriding base class methods must be used with care, however, to avoid unintentionally hiding overloaded methods – a single overriding method in a derived class will hide all overloaded methods of that name in the base class!

![](bbox=[0.118, 0.262, 0.19, 0.307])

override.cpp

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.
+   
+   ```cpp
+   #include <string>
+   #include <iostream>
+   using namespace std ;
+   ```

+   2. Declare a class named “Man”, which will be a base class.
+   
+   ```cpp
+   class Man
+   {
+       // Class members go here.
+   };
+   ```

+   3. Between the braces of the Man class declaration, insert a public access specifier and an inline output method.
+   
+   ```cpp
+   public:
+       void speak() { cout << “Hello! ” << endl ; }
+   ```

+   4. Now, insert an overloaded inline output method.
+   
+   ```cpp
+   void speak( string msg )
+       { cout << “ ” << msg << endl ; }
+   ```

+   5. After the Man class declaration, declare a class named “Hombre” that is derived from the Man class.
+   
+   ```cpp
+   class Hombre : public Man
+   {
+       // Class members go here.
+   };
+   ```

![](bbox=[0.118, 0.686, 0.207, 0.747])

The method declaration in the derived class must exactly match that in the base class to override it – including the const keyword if it is used.

+   6. Between the braces of the Hombre class declaration, insert an access specifier and a method that overrides the overloaded base class method – without a tab output.
+   
+   ```cpp
+   public:
+       void speak( string msg ) { cout << msg << endl ; }
+   ```

+   7. After the Hombre class declaration, add a main method containing a final **return** statement and creating two objects – an instance of the base class and an instance of the derived class.
+   
+   ```cpp
+   int main()
+   {
+   ```