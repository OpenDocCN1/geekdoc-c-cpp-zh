The opposite behavior is expected when we explicitly implement `Perimeter.Size()` and provide a normal implementation for the `Size()` method. This is illustrated as ShapeH, as included in the full code listing in the appendix.

The full code listing also includes another example, in the namespace MI2, where the interfaces include default implementations for the `Size()` method. The behavior of various classes implementing the two interfaces can be more or less "predicted" based on what we have learned so far. We will leave it to the readers to verify their "intuitions".

So, what is the takeaways of this lesson?

First, do not use the interface default implementations. When you create a new interface, do not even think about using default implementations. [smile] As stated, if you need to share some common implementations, consider using an (abstract) base class.

When you feel the impulse to add a method or property, with or without a default implementation, to an existing interface, don't! Just don't! [icon] Interfaces are supposed to be immutable. No matter what.

Second, there may be legit cases where you will have to implement an interface method explicitly. For example, when there is a name collision when implementing multiple interfaces, you can implement one method/property in the normal way, as in our examples of Shape1G and Shape1H, and explicitly implement the rest.

# 23.3. Pair Programming - XML Doc Comments

One last thing we need to learn in this lesson is the XML documentation feature of C#.

This is originally based on JavaDoc, as is the case with many other programming languages, and it allows us to embed documentations in the code, within comments. This is called the "doc comment".