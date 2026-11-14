Nonfunctional specifications have to be added; we use these to explain constraints such as:

+   - Performance and timing constraints
+   - Dependability constraints
+   - Cost, implementation, and manufacturing constraints.

Whereas the Requirements Specification provides a view from the outside of the system looking in, the Design Specification provides a view from the inside looking out as well.

Notice also that the Design Specification has two masters:

+   - It must specify the system's public interface from inside the system.
+   - It must specify how well the requirements defined for and by the public interface are to be met by the internal functions of the system.

The specification is written in the designer's language and from the designer's point of view. It serves as a bridge between the customer and the designer, as we see in Figure 9.26.

![](bbox=[0.276, 0.35, 0.48, 0.6])

Figure 9.26 The Customer, the Requirements, the Design, and the Engineer

We have seen that the Requirements Specification is written in less formal terms with the intent of capturing the customer's view of the product. The Design Specification must formalize those requirements in precise, unambiguous language.

Putting the inevitable changes that occur during the lifetime of any project aside for the moment, we find that the design specification should be sufficiently clear, robust, and complete that a group of engineers could develop the product without ever talking to the author of the specification.

> **Design Note**
> 
> A good litmus test of the viability of a design specification is the question, “If I send this to my colleague (who is working for one of our subcontractors in another country), will he or she understand this?” If the answer is no, the specification should be reexamined.