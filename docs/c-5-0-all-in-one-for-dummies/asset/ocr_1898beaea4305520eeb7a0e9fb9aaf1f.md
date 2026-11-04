allowed from other classes in the assembly. This solution may not be ideal, but it should be more secure — if that's a consideration.

# ## Protected internal: Being a more generous protector

Making items in the BankAccount base class protected internal, rather than just protected, simply adds a new dimension to the accessibility of those items in your program. Using protected alone allows a subclass (in any assembly in the program) to access protected items in the base class. Adding internal extends the items' accessibility to any class, as long as it's in the same assembly as BankAccount or at least a subclass in some other assembly.

![](bbox=[0.146, 0.341, 0.221, 0.393])

In the ProtectedInternalLimitsAccess example on http://csharp102.info, you can see this effect. The class AnotherClass that's defined within BankAccount's own assembly can access the protected internal set accessor in the Balance property. However, the nearly identical AnotherClass in a different assembly cannot access Balance's set accessor to set the balance.

![](bbox=[0.146, 0.461, 0.221, 0.521])

Make items as inaccessible as possible. Start with private. If some parts of your code need more access than that, increase it selectively. Maybe just protected will work (that's all a subclass needs). Maybe other classes in the same assembly truly do need access. If so, increase it to internal. If subclasses and other classes in the same assembly need access, use protected internal. Use public only for classes (and their members) that should be accessible to every class in the program, regardless of assembly.

![](bbox=[0.146, 0.589, 0.221, 0.649])

The same advice that applies to whole classes also applies to class members: Keep them as inaccessible as possible. Little *helper classes*, or classes that support the implementation of more public classes, can be limited to no more than internal.

If a class or other type needs to be private, protected, or protected internal, nest it, if you can, inside the class that needs access to it.

# ## Putting Classes into Namespaces

Namespaces exist to put related classes in one bag and to reduce collisions between names used in different places. For example, you may compile all math-related classes into a MathRoutines namespace.

![](bbox=[0.146, 0.836, 0.221, 0.896])

A single file can be (but isn't commonly) divided into multiple namespaces: