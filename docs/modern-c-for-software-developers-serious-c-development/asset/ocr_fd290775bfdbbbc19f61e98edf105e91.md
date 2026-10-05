```
float pif = Circle::pi
and:
Circle::multiply(Circle::pi)
```

**Note:** A static member function cannot call a non-static member function.

# Static Data Members

The declaration of a static data member in a class declaration is not a definition. The static data member must be initialized (defined) outside of the class declaration and at namespace scope.

```
class Square
{
public:
  static float length;
}
Square::length = 5;
```

However, if the static data member is const, can it initialized in the class declaration:

```
class Circle
{
public:
  static const float pi = 3.14;
}
```

If a static data member is declared as private then it will be inaccessible outside the class. There are two ways to initialize this variable. Firstly, we can declare the data member as const and initialize it inside the class declaration. Secondly, we can specify a public static member function that initializes the private data member. A static member function has access to all of the public and private data members of the class.