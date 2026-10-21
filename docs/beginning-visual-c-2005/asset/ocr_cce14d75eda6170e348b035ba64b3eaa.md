# C++/CLI Programming

All C++/CLI classes, including classes that you define, are derived classes by default. This is because both value classes and reference classes have a standard class, System::Object, as a base class. This means that both value classes and reference classes inherit from the System::Object class and therefore have the capabilities of the System::Object class in common. Because the ToString() function is defined as a virtual function in System::Object, you can override it in your own classes and have the function called polymorphically when required. This is what you have been doing in previous chapters when you defined the ToString() function in a class.

The System::Object base class for all value class types is also responsible for enabling the boxing and unboxing of values of the fundamental types. This process means that values of the fundamental types can behave as objects, but can participate in numerical operations without carrying the overhead of being objects. Values of the fundamental types are stored just as values for the purposes of normal operations and are only converted to an object that is referenced by a handle of type System::Object^ when they need to behave as objects. Thus you get the benefit of being able to treat fundamental values as objects when you need to without incurring the overhead of them being objects in general.

# Inheritance in C++/CLI Classes

Although value classes always have the System::Object class as a base, you cannot define a value classes derived from an existing class. To put it another way, when you define a value class you are not allowed to specify a base class. This implies that polymorphism in value classes is limited to the functions that are defined as virtual in the System::Object class. These are the virtual functions that all value classes inherit from System::Object:

| Function | Description |
|---|---|
| String^ ToString() | Returns a String representation of an object and the implementation in the System::Object class returns the class name as a string. You would typically override this function in your own classes to return a string representation of the value of an object. |
| bool Equals(Object^ obj) | Compares the current object to obj and returns true if they are equal and false otherwise. Equal in this case means referential equality — that is the objects are one and the same. Typically you would override this function in your own classes to return true when the current object is the same value as the argument — in other words, when the fields are equal. |
| int GetHashCode() | Returns an integer that is a hash code for the current object. Hash codes are used as keys to store objects in a collection that stores (key,object) pairs. Objects are subsequently retrieved from such a collection by supplying the key that was used when the object was stored. |

Of course, because System::Object is also a base class for reference classes you may want to override these functions in reference classes too.