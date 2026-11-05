# Example 11-24

```
```csharp
// Calls overridden ToString( ) defined in Person class
// Returns the first name, a space, and the last name
this.txtBxName.Text = aStudent.ToString( );

// Calls ToString( ) defined in object class
// Returns a number representing age in a string format
this.txtBxAge.Text = aStudent.Age.ToString( );
```
```

As is noted in the comment, the first call to the `ToString( )` method calls the method defined in the `Person` class. Remember that the method overrides the object’s `ToString( )`. This implementation of `ToString( )` (included in Example 11-9) was to concatenate the first and last name with a space between them. The CLR recognized that it should use this method because it was called with a `Student` object. Student did not contain an implementation of the `ToString( )` method; thus, the CLR looked next to the class from which it had been derived, the `Person` class.

The second call to the `ToString( )` method does not use the Person class’s implementation. Notice that this call is made with an `int` object. The Age property returns an `int`. Thus, based on the `object` making the call, the `ToString( )` method from the Object class is called.

Polymorphism allows a method of a `class` to be called without regard to what specific implementation it provides. Thus, in .NET, polymorphism is implemented through interfaces, inheritance, and the use of abstract classes.

# Polymorphic Programming in .NET

As you saw, multiple classes can implement the same `interface` or implement more than one `interface`. The `interface` describes the methods and the types of parameters each method member needs to receive and return, but it leaves the actual details of the body of the method up to the classes that implement the `interface`. Every `class` that implements the `interface` may have a completely different behavior. The method name is the same in all the classes implementing the `interface`, but the functionality can be much different from one `class` to another.

![](bbox=[0.174, 0.744, 0.237, 0.794])

The black box concept of object-oriented development comes into play here. You do not have to know how the method goes about doing its work. All you have to know is what arguments to send, if any, and what you expect to be accomplished when the object finishes its work. That may be a return value or just an indication that the method is complete.

Through inheritance, polymorphism is made possible by allowing classes to override base class members. This makes **dynamic binding** possible. The CLR determines which method to call at run time based on which `object` calls the method. Marking the method with the `virtual` keyword enables derived classes to write their own functionality for the method.