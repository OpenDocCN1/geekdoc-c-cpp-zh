Moving the member definitions outside of the class definition like this makes it easier to get a quick overview of the class's (public) interface. This is particularly interesting for member functions that have longer function bodies, or for classes with a larger number of members.

You can then put the definitions of the members of Box somewhere after the definition of their class. The name of each member must be qualified with the class name so the compiler knows to which class they belong:

```
```cpp
// Constructor definition
Box::Box(double length, double width, double height)
{
  std::cout << "Box constructor called." << std::endl;
  m_length = length;
  m_width = width;
  m_height = height;
}
```
```

```
```cpp
// Member function definition
double Box::volume()
{
  return m_length * m_width * m_height;
}
```
```

Ex12_02.cpp puts it all together for you: The Box class definition, followed by these two member definitions, and a main() function. This main() function is the exact same one as in Ex12_01.cpp.

> > **Note** This separation of a class's interface and implementation is completely analogous to that for modules in the previous chapter, in terms of both motivation and technical implications. Unsurprisingly, out-of-class member function definitions can of course also be moved to implementation files, leaving only the class definition in the interface file (be it a header or a module interface file). We discuss this further later after this section on constructors.

# Default Arguments for Constructor Parameters

When we discussed “ordinary” functions, you saw that you can specify *default values* for the parameters in the function prototype. You can do this for class member functions, including constructors. Default parameter values for constructors and member functions always go inside the class, not in an external constructor or function definition. We can change the class definition in the previous example to the following:

```
```cpp
class Box
{
public:
  // Constructors
  Box() = default;
  Box(double length = 1.0, double width = 1.0, double height = 1.0);

  double volume();   // Function to calculate the volume of a box
```
```