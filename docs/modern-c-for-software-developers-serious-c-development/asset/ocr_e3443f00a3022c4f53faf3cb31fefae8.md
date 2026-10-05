# C++ Templates: Generic Classes

A class template is a family of classes where the actual type of the data that is manipulated in the class is specified as a generic parameter.

Class templates are useful when classes use logic that can be generalized. For example, the algorithm that maintains a queue of integers will also work for a queue of characters.

When we create a class template, it can perform the operation we define, such as maintaining a queue or a linked list, for any type of data. The compiler will automatically create the correct type of object at compile-time, based upon the type we specify when the object is instantiated.

The general form of a class template declaration is:

```
template <Ttype>
class class-name {
.
}
```

This is a declaration and not a definition. Since the parameter Type is a generic type, this declaration declares a family of classes parameterized on Type. A definition instantiates an object using a particular template type.

A specific class is instantiated when a particular Type (template type) is specified. If necessary, we can specify more than one generic data type in a template declaration using a comma-separated list of template types.