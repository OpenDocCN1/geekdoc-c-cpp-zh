The next try block then defines an Array<> object that can store Box objects. The compiler generates a second instance of the class template, Array<Box>, because the template has not been instantiated for Box objects previously. The statement also calls the constructor to create the boxes object, so an instance of the function template for the constructor is created. The constructor for the Array<Box> class calls the default constructor for the Box class when the m_elements member is created in the free store. All the Box objects in the m_elements array therefore have the default dimensions of 1x1x1.

The volume of each Box object in boxes is output in a final for loop. The boxes[i] expression calls the overloaded subscript operator, so the compiler instantiates this template a second time as well. When i has the value numBoxes the subscript operator function throws an exception because an index value of numBoxes is beyond the end of the m_elements array. The catch block following the try block catches the exception. Because the try block is exited, all locally declared objects will be destroyed, including the boxes object.

# # Non-Type Class Template Parameters

A non-type parameter looks like a function parameter—a type name followed by the name of the parameter. Here's an example:

```
```cpp
template <typename T, size_t size>
class ClassName
{
    // Definition using T and size...
};
```
```

This template has a type parameter, T, and a non-type parameter, size. The definition is expressed in terms of these two parameters and the template name.

You cannot use just any type as the type of a non-type template parameter. Most class types in particular are not allowed. That is, you cannot use types such as Box or std::string for a non-type template parameter. The type of a non-type template parameter is nearly always a fundamental type (size_t, long, bool, char, float, and so on—only not void), enumeration type, pointer type, or reference type (this includes pointers and references to functions).

If you need it, the type for a non-type parameter can also be the type name of a preceding type parameter:

```
```cpp
template <typename T,     // T is the name of the type parameter
          T value>        // T is also the type of this non-type parameter
class ClassName
{
    // Definition using T and value...
};
```
```

The parameter T must appear before its use in the parameter list, so value couldn't precede the type parameter T here. Of course, using a type parameter as the type of a non-type parameter implicitly restricts the arguments for T to the aforementioned types that are allowed for non-type parameters.

^a As of C++20, you can in principle use certain class types (a specific subset of so-called literal classes, to be exact), but the restrictions on these class types are so severe we won't discuss this possibility.