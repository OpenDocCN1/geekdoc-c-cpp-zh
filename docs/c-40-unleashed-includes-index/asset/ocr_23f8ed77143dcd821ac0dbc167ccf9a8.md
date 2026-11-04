overview of its concepts. After covering functional programming from this more theoretic angle, we apply the concept to the use of delegates in C#.

# Historical Perspective

Object-oriented programming provides a means to tackle various aspects of complexity that arise during the creation and maintenance of applications. It does so through various means, such as encapsulation of state and polymorphism, stimulating reuse of existing functionality through class hierarchies.

If we go one level up from object-oriented programming, we find ourselves back in the world of procedural programming, where a different sort of complexity is dealt with. By stimulating the use of procedures (methods) to reuse blocks of code, parameterized by some inputs, excessive duplication of code is avoided.

We can continue our way up the chain, landing at structured programming, where the use of low-level goto statements is strongly discouraged, in favor of control flow primitives such as loops and conditional statements. Again, this deals with complexities that arise from the creation and maintenance of nontrivial pieces of code.

Before we go any further with our discussion, you need to understand that the paradigms mentioned are not mutually exclusive. Indeed, C# fits nicely in all of those camps. You could go as far as saying that OO-languages derive from procedural languages, extending it with the concept of classes and such. Similarly, procedural languages extend the functionality their structured parents have to offer by adding the concept of procedures.

While walking this inheritance chain of language paradigms, we’ve ended up close to the hardware of the underlying machine. Structured programming languages essentially provide abstractions over low-level machine primitives like branches, among others. Going back to object-oriented programming, we see layers of abstraction are added to continue to simplify the creation of applications of increasing complexity. You can compare this to the rings of an onion, around low-level assembler languages, as shown in Figure 17.1.

![](bbox=[0.12, 0.8, 0.45, 0.97])