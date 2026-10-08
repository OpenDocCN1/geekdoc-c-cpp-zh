# Declaring Objective-C Types 21

always referenced by pointer.

In the first implementations of Objective-C, which produced pure C from Objective-C, classes were turned into structure definitions describing the layout of the objects. You can still see some legacy of this in GCC error messages, which will occasionally refer to objects as “structures.

In C, you need an explicit cast to turn any structure pointer into any other kind of structure pointer. This rule is relaxed slightly for Objective-C. The layout of any object is defined by the instance variables (ivars) in the root class, then by the instance variables in each subsequent class down the hierarchy. Subclasses can only add new instance variables, not remove or rearrange ones from the superclasses. This means that it is always safe, in terms of memory layout, to cast a pointer to an instance of one class to a pointer to an instance of a superclass. It is also safe from the perspective of the object-oriented type system; any subclass will always respond to all the messages that the superclass responds to.

Object pointers in Objective-C are identified by the name of the class, followed by a star, just as structure pointers are in C, although without the struct keyword. You can always cast a pointer to an instance of its superclass implicitly. This works even for indirect superclasses. For example, NSMutableArray is a subclass of