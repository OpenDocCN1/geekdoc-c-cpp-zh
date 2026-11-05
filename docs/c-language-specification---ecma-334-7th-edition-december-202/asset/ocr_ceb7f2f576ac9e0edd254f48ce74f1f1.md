```
}
}
```

the C and D classes contain two virtual methods with the same signature: The one introduced by A and the one introduced by C. The method introduced by C hides the method inherited from A. Thus, the override declaration in D overrides the method introduced by C, and it is not possible for D to override the method introduced by A. The example produces the output:

B, F
B, F
D, F
D, F

Note that it is possible to invoke the hidden virtual method by accessing an instance of D through a less derived type in which the method is not hidden.

*end example*

# 15.6.5 Override methods

When an instance method declaration includes an override modifier, the method is said to be an override method. An override method overrides an inherited virtual method with the same signature. Whereas a virtual method declaration introduces a new method, an override method declaration specializes an existing inherited virtual method by providing a new implementation of that method.

The method overridden by an override declaration is known as the overridden base method For an override method M declared in a class C, the overridden base method is determined by examining each base class of C, starting with the direct base class of C and continuing with each successive direct base class, until in a given base class type at least one accessible method is located which has the same signature as M after substitution of type arguments. For the purposes of locating the overridden base method, a method is considered accessible if it is public, if it is protected, if it is protected internal, or if it is either internal or private protected and declared in the same program as C.

A compile-time error occurs unless all of the following are true for an override declaration:

+   - An overridden base method can be located as described above.
+   - There is exactly one such overridden base method. This restriction has effect only if the base class type is a constructed type where the substitution of type arguments makes the signature of two methods the same.
+   - The overridden base method is a virtual, abstract, or override method. In other words, the overridden base method cannot be static or non-virtual.
+   - The overridden base method is not a sealed method.
+   - There is an identity conversion between the return type of the overridden base method and the override method.
+   - The override declaration and the overridden base method have the same declared accessibility. In other words, an override declaration cannot change the accessibility of the virtual method. However, if the overridden base method is protected internal and it is declared in a different assembly than the assembly containing the override declaration then the override declaration's declared accessibility shall be protected.
+   - The override declaration does not specify any type_parameter_constraints_clauses. Instead, the constraints are inherited from the overridden base method. Constraints that are type parameters in