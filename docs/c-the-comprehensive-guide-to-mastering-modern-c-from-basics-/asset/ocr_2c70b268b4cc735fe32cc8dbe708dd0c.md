# 23.5 Template Classes

The template technique, as you have just learned with function templates, is not limited to functions but can also be used with classes. To be precise, C++ would be as popular and beloved as it is today without class templates. The standard library defines many class templates, of which you have already used std::vector or std::string. With std::vector, you specified the type in the angle brackets. std::string, on the other hand, is an instantiation of the char type and is internally defined as follows:

```
using string = basic_string<char>;
```

In addition to the standard container classes like std::vector, std::list, and so on, the stream classes for input/output (see Chapter 26) are also mostly implemented as instantiations of char.

23.5.1 Implementing Class Templates To start, I want to show how you can create a very primitive container (a container class) that can hold (almost) any type. The introduction of a class template here again uses the following statement:

```
template <typename T>
```