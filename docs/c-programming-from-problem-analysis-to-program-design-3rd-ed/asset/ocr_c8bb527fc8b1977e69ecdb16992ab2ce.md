Remember that a `class` does not have to `override` a `virtual` method. The `class` can choose to use the base class’s implementation.

Because an `abstract class` cannot be instantiated, the features of both interfaces and inheritance come into play with polymorphic programming. Through the use of abstract classes, classes that derive from them are forced to include implementation details for any abstract method. Unlike interfaces, which simply provide the heading for the methods that have to be implemented, some or all of the members of an abstract class can be implemented. Abstract classes can also include data members, properties, events, and methods. The methods can be marked as `virtual` or as `abstract`, or be completely implemented. The determination of which method to use is based on the `object` that makes the call.

Inheritance is very useful for adding to the functionality of an existing `class` without having to reinvent the wheel with each new application. With .NET, you have to remember that you only have single inheritance. A `class` can implement multiple interfaces, but it must provide the implementation details for all of the interface’s methods. Component programming is probably the way of the future for development. It is a powerful technique that enables you to implement the multiple interfaces of an `object` easily. The common goal of all these advanced object-oriented features is to enable polymorphic programming.

Another programming technique, generics, reduces duplication of code through writing common functions or types that differ only in the set of types on which they operate. Generics enables algorithms to be written where a number of details, including the data type can be “specified-later”. Generics is the topic of the next section.

# Generics

Generics reduce the need to rewrite algorithms for each data type. You can create generic classes, delegates, interfaces, and methods. With each of these, you identify where data will change in the code segment by putting a placeholder in the code for the type parameters. A generic `class` might use placeholder(s) for the data type of its instance data members or placeholders for return types of one or more of its methods. After the generic `class` is defined, it could be instantiated using several different types of data.

A generic method might use a generic type for one of its formal parameters and/or use a generic type as the type of its return value. Generic methods can be defined both as part of generic and other classes. First examine what is involved in defining a generic class.

# Generic Classes

Prior to the introduction of generics, one way to write reusable code was to use the `object` data type for instance data members. You will recall that `object` is the base class from which all other classes are derived. After the data type is defined as an object, then