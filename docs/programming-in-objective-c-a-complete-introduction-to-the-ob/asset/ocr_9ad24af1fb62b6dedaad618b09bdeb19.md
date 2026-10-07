# Asking Questions About Classes

if one method returned an object and the other returned an integer, for example. If the inconsistency between two methods is just a different type of object (for example, the Fraction's add: method takes a Fraction object as its argument and returns one, and the Complex's add: method takes and returns a Complex object), the compiler will still generate the correct code because (this, pointers) are passed as references to objects anyway.

# Asking Questions About Classes

As you start working with variables that can contain objects from different classes, you might need to ask questions such as the following:

+   - Is this object a rectangle?
- Does this object support a print method?
- Is this object member of the Graphics class or one of its descendants?

You can use the answers to these questions to execute different sequences of code, avoid an error, or check the integrity of your program while it's executing.
Table 9.1 summarizes some of the basic methods that the NSObject class supports for these types of questions. In this table, class-object is a class object (typically generated with the class method), and selector is a value of SEL type

# Table 9.1 Methods for Working with Dynamic Types

| Method | Question or Action |
|---|---|
| (BOOL) isKindOfClass:class-object | Is the object member of class-object or a descendant? |
| (BOOL) isMemberOf:class-object | Is the object member of class-object? |
| (BOOL) respondsToSelector:selector | Can the object respond to the method specified by selector? |
| (+BOOL) instancesRespondToSelector:selector | Can instances of specified class respond to selector? |
| (+BOOL) isSubclassOf:class-object | Is the object a subclass of the specified class? |
| (id) performSelector:selector | Apply the method specified by selector. |
| (id) performSelector:withObject:object | Apply the method specified by selector, passing the argument object. |
| (id) performSelector:withObject:object1withObject:object2 | Apply the method specified by selector with the arguments object1 and object2. |