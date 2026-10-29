# Friend Classes

**friend class**

A class can be a **friend** of another class in the same way that a function can be a friend of a class. If the class F is a friend of the class C, then every member function of the class F is a friend of the class C. To make one class a friend of another, you must declare the friend class as a friend within the other class.

**forward declaration**

When one class is a friend of another class, it is typical for the classes to reference each other in their class definitions. This requires that you include a **forward declaration** to the class defined second, as illustrated in the outline that follows this paragraph. Note that the forward declaration is just the heading of the class definition followed by a semicolon.

```
## Friend Functions

A friend function of a class is an ordinary function except that it has access to the private members of objects of that class. To make a function a friend of a class, you must list the function declaration for the friend function in the class definition. The function declaration is preceded by the keyword friend. The function declaration may be placed in either the private section or the public section, but it will be a public function in either case, so it is clearer to list it in the public section.

### SYNTAX OF A CLASS DEFINITION WITH FRIEND FUNCTIONS

```cpp
class Class_Name
{
public:
    friend Declaration_for_Friend_Function_1
    friend Declaration_for_Friend_Function_2
    .
    .
    Member_Function_Declarations
private:
    Private_Member_Declarations
};
```

### EXAMPLE

```cpp
class FuelTank
{
public:
    friend void fillLowest(FuelTank& t1, FuelTank& t2);
    //Fills the tank with the lowest fuel level, or et al if a tie.

    FuelTank(double theCapacity, double theLevel);
    FuelTank();
};
```
```

![](bbox=[0.652, 0.505, 0.8496, 0.584])