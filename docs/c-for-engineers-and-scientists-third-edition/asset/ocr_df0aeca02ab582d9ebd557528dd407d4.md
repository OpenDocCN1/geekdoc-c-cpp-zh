# Abstract Data Types

To gain a clear understanding of what an abstract data type is, take another look at the built-in data types in C++ integers, doubles, Boolean, and characters. In using these data types, typically you declare one or more variables of the desired type, use them in accepted ways, and avoid using them in ways that aren't specified. For example, you use the modulus operator on double-precision numbers. Because this operation makes no sense for double-precision numbers, it's never defined, in any programming language, for each data type consists of both a type of data, such as integer or double, and specific capabilities.

In computer terminology, the relation of data and associated operations is defined as a data type. That is, a data type defines both the types of data and the operations that can be performed on it. In this light, the integer type, the double-precision data type, and the character type provided in C++ are all examples of built-in data types defined by a type of data and specific operational capabilities for initializing and manipulating it. In a simple form, this relationship can be described as follows:

Data Type = Allowable Data Values + Operational Capabilities

Therefore, the operations you have been using in C++ are an inherent part of each data type you have been using. For each of these data types, C++ designers would have to carefully consider and implement specific operations.

To understand the importance of the operational capabilities a programming language provides, take a moment to review a list of capabilities supplied with C++'s built-in data types (int, double, and char). Table 10.1 lists the minimum set of such capabilities.

Table 10.1 C++ Built-In Data Type Capabilities
| Capability | Example |
| --- | --- |
| Define one or more variables of the data type | int a, b; |
| Initialize a value at definition | int a = 5; |
| Assign a value to a variable | a = 10; |
| Assign one variable's value to another variable | a = b; |
| Perform mathematical operations | a = a + b |
| Convert from one data type to another | a = int (7.2); |

Now see how this information relates to abstract data types (ADTS). By definition, an abstract data type is simply a user-defined type that defines both a type of data and the operations that can be performed on it. User-defined data types are required when you want to create objects that are more complex than simple integers and characters. To create your own data types, you must be aware of the type of data you're creating and the capabilities you provide to initialize and manipulate the data.

As a specific example, say you're programming an application that uses data extensively. Clearly, from a data standpoint, a date must be capable of accessing and storing a month, day, and year designation. From an implementation standpoint, there are several ways of