# 9.5 Designing for Inheritance

Throughout this chapter, several design issues have been addressed in the discussion of the nuts and bolts of inheritance in Java. The following list summarizes some of the inheritance issues that you should keep in mind during the program design stage:

+   - Every derivation should be an is-a relationship. The child should be a more specific version of the parent.
+   - Design a class hierarchy to capitalize on reuse, and potential reuse in the future.
+   - As classes and objects are identified in the problem domain, find their commonality. Push common features as high in the class hierarchy as appropriate for consistency and ease of maintenance.
+   - Override methods as appropriate to tailor or change the functionality of a child.
+   - Add new variables to the child class as needed, but don’t shadow (redefine) any inherited variables.
+   - Allow each class to manage its own data. Therefore use the super reference to invoke a parent’s constructor and to call overridden versions of methods if appropriate.
+   - Use interfaces to create a class that serves multiple roles (simulating multiple inheritance).
+   - Design a class hierarchy to fit the needs of the application, with attention to how it may be useful in the future.
+   - Even if there are no current uses for them, override general methods such as toString and equals appropriately in child classes so that the inherited versions don’t cause unintentional problems later.
+   - Use abstract classes to specify a common class interface for the concrete classes lower in the hierarchy.
+   - Use visibility modifiers carefully to provide the needed access in derived classes without violating encapsulation.



We’ve seen the final modifier used in declarations to create constants many times. The other uses of the final modifier involve inheritance and can have a significant influence on software design. Specifically, the final modifier can be used to curtail the abilities related to inheritance.

Earlier in this chapter we mentioned that a method can be declared as final, which means it cannot be overridden in any classes that extend the one it is in. A final method is often used to insist that particular functionality be used in all child classes.

> **KEY CONCEPT**
> 
> The final modifier can be used to restrict inheritance.