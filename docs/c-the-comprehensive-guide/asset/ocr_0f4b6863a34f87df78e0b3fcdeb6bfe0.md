+   - Besides the non-inline code of the method, the function call hinders any cross-function optimization by the compiler and acts as a time-consuming synchronizing barrier in multithreading.
+   - The pointer to the virtual method table is not negligible in small (and numerous) data structures.
+   - A virtual method should never be called in a constructor (and should not be called in a destructor).

There is also a less technical matter to consider. What if you never override a virtual method? Well, then you shouldn't have made it virtual in the first place, right? Oh, you wanted to provide a configuration point in a library? That's good, it allows for extensibility. But now someone comes along who uses your library and actually extends it. Can the virtual method still fulfill its task? No idea, right? It's no longer your virtual method being called, but the method of the extender. This is fundamentally good, but it is a responsibility not to be underestimated. Whose? The overrider's? No—yours! You should and may only allow a method to be overridden using virtual if you make it difficult for extenders to misuse the class—despite the “invasive” code of an extender.

With final, it's even worse. When you write final on a method, you are implicitly saying that the behavior of the object will not change anymore. But do you also adhere to it? Do you call another virtual method in the final method? How can you then say that the method still does what it is supposed to do? Have you specified preconditions, postconditions, or invariants for this final method? You will find it difficult to guarantee these if you call other virtual methods from your final method.

Don't get me wrong: sometimes final is just a form of documentation, but technically speaking, you are on thin ice with the promise that “this method does exactly what I say” if you call another virtual method. Therefore use final, yes, but within limits.

# Relevant Guidelines

This is a list of the guidelines most relevant to virtual methods:

+   - C.2: Use class when the class has an invariant; use struct when the data members can vary independently.
+   - C.3: Represent the distinction between an interface and an implementation by using a class. [For example, it is easier to encapsulate data and highlight methods as interfaces with a class than if you only use free functions.]
+   - C.8: Use class rather then struct if any member is not public.
+   - C.9: Minimize the exposure of members.
+   - C.35: A base class destructor should be either public and virtual or protected and nonvirtual.
+   - C120: Use class hierarchies to represent concepts with an inherent hierarchical structure (only).