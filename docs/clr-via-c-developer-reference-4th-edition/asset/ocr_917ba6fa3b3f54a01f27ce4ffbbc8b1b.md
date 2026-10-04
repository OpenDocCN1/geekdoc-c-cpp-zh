# CHAPTER 8

# Methods

+   In this chapter:
Instance Constructors and Classes (Reference Types) ........... 181
Instance Constructors and Structures (Value Types) ................... 184
Type Constructors ............................................................ 187
Operator Overload Methods ................................. . . . . . . . . . 191
Conversion Operator Methods . . . . . . . . . . . . . . . . . . . . . 195
Extension Methods ............................................................ 198
Partial Methods ................................................................................ 204

This chapter focuses on the various kinds of methods that you'll run into, including instance constructors and type constructors, as well as how to define operators and type conversions (for implicit and explicit casting). We'll also talk about extension methods, which allow you to logically add your own instance methods to already existing types, and partial methods, which allow you to spread a type's implementation into multiple parts.

# Instance Constructors and Classes (Reference Types)

Constructors are special methods that allow an instance of a type to be initialized to a good state. Constructor methods are always called .ctor (for constructor) in a method definition metadata table. When creating an instance of a reference type, memory is allocated for the instance's data fields, the object's overhead fields (type object pointer and sync block index) are initialized, and then the type's constructor is called to set the initial state of the object.

When constructing a reference type object, the memory allocated for the object is always zeroed before the type's constructor is called. Any fields that the constructor doesn't explicitly overwrite are guaranteed to have a value of 0 or null.

Unlike other methods, instance constructors are never inherited. That, a class has only the instance constructors it defines. Because instance constructors are not inherited, you cannot apply the following modifiers to an instance constructor: virtual, new, override, sealed, or abstract. If you define a class that does not explicitly define any constructors, the C# compiler defines a default (parameterless) constructor for you whose implementation simply calls the base class's parameterless constructor.