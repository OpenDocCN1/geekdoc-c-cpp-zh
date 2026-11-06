
## 33. Prefer minimal classes to monolithic classes.

### Summary

Divide and conquer: Small classes are easier to write, get right, test, and use. They are also more likely to be usable in a variety of situations. Prefer such small classes that embody simple concepts instead of kitchen-sink classes that try to implement many and/or complex concepts (see Items 5 and 6).

### Discussion

Designing fancy large classes is a typical mistake when starting object-oriented design. The prospect of having a class that offers complete and complex functionality in one shot can be quite alluring. However, designing smaller, minimal classes that can be easily combined is an approach that is more successful in practice for systems of any size, for many reasons:

- A minimal class embodies one concept at the right level of granularity. A monolithic class is likely to embody several separate concepts, and using one implies dragging the intellectual overhead of all others. (See Items 5 and 11.)
- A minimal class is easier to comprehend, and more likely to be used and reused.
- A minimal class is easier to deploy. A monolithic class must often be deployed as a bulky indivisible unit. For example, a monolithic *Matrix* class might attempt to implement and deploy exotic functionality such as computing the eigenvalues of a matrix—even when the majority of clients just want simple linear algebra. A better packaging would implement various functional areas as non-member functions operating on a minimal *Matrix* type. Then the functional areas can be tested and deployed in separation to the callers who need them. (See Item 44.)
- Monolithic classes dilute encapsulation. When a class has many member functions that don't need to be members but are—and therefore have gratuitous visibility to the class's private implementation—then the class's private data members become nearly as bad as public variables.
- Monolithic classes usually result from an attempt to predict and deliver a "complete" solution to a problem; in practice, they virtually never succeed. There's always something more that people want—and something less, for that matter.
- Monolithic classes are harder to make correct and error-safe because they often tackle multiple responsibilities. (See Items 5 and 44.)

### References

*[Cargill92]* pp. 85-86, 152, 174–177 • *[Lakos96]* §0.2.1–2, §1.8, §8.1–2 • *[Meyers97]* §18 • *[Stroustrup00]* §16.2.2, §23.4.3.2, §24.4.3 • *[Sutter04]* §37–40

## 34. Prefer composition to inheritance.

### Summary

Avoid inheritance taxes: Inheritance is the second-tightest coupling relationship in C++, second only to friendship. Tight coupling is undesirable and should be avoided where possible. Therefore, prefer composition to inheritance unless you know that the latter truly benefits your design.

### Discussion

Inheritance is often overused, even by experienced developers. A sound rule of software engineering is to minimize coupling: If a relationship can be expressed in more than one way, use the weakest relationship that's practical.

Given that inheritance is nearly the strongest relationship we can express in C++, second only to friendship, it's only really appropriate when there is no equivalent weaker alternative. If you can express a class relationship using composition alone, you should prefer that.

In this context, “composition” means simply embedding a member variable of a type within another type. This way, you can hold and use the object in ways that allow you control over the strength of the coupling.

Composition has important advantages over inheritance:

- *Greater flexibility without affecting calling code:* A private data member is under your control. You can switch from holding it by value to holding by (smart) pointer or Pimpl (see Item 43) without breaking client code; you would only need to change the implementations of the class's own member functions that use it. If you decide you need different functionality, you can easily change the type of the member or the manner of holding it while keeping the class's public interface consistent. In contrast, if you begin with a public inheritance relationship, it is likely that clients have already come to depend on the inheritance; you have therefore committed your class to it and cannot easily change your base class decision later on. (See Item 37.)
- *Greater compile-time insulation, shorter compile times:* Holding an object by pointer (preferably a smart pointer), rather than as a direct member or base class, can also allow you to reduce header dependencies because declaring a pointer to an object doesn't require that object's full class definition. By contrast, inheritance always requires the full definition of the base class to be visible. A common technique is to aggregate all private members behind a single opaque pointer, called a Pimpl (see Item 43).
- *Less weirdness:* Inheriting from a type can cause name lookup to pull in functions and function templates defined in the same namespace as that type. This is very subtle and hard to debug. (See also Item 58.)
- *Wider applicability:* Some classes were not designed to be bases in the first place (and see Item 35). Most classes, however, can fulfill the role of a member.
- *Great robustness and safety:* The tighter coupling of inheritance makes it more difficult to write error-safe code. (See [Sutter02] §23.)
- *Less complexity and fragility:* Inheritance exposes you to additional complications, such as name hiding and other complications that can arise in the presence of later changes to the base class.

Of course, these are not arguments against inheritance *per se*. Inheritance affords a great deal of power, including substitutability and/or the ability to override virtual functions (see Items 36 through 39, and Exceptions below). But don’t pay for what you don’t need; unless you need inheritance’s power, don’t endure its drawbacks.

### Exceptions

Do use public inheritance to model substitutability. (See Item 37.)

Even if you don’t need to provide a substitutability relationship to all callers, you do need *nonpublic* inheritance if you need any of the following, in rough order from most common (the first two points) to exceedingly rare (the rest):

- If you need to override a virtual function.
- If you need access to a protected member.
- If you need to construct the used object before, or destroy it after, a base class.
- If you need to worry about virtual base classes.
- If you *know* you benefit from the empty base class optimization, including that it matters in this case and that your target compiler(s) actually perform it in this case. (See Item 8.)
- If you need controlled polymorphism. That is, if you need a substitutability relationship, but that relationship should be visible only to selected code (via friendship).

### References

[Cargill92] pp. 49-65, 101-105 • [Cline99] §5.9-10, 8.11-12, 37.04 • [Dewhurst03] §95 • [Lakos96] §17, §6.3.1 • [McConnell93] §5 • [Meyers97] §40 • [Stroustrup00] §24.2-3 • [Sutter00] §22-24, §26-30 • [Sutter02] §23

## 35. Avoid inheriting from classes that were not designed to be base classes.

### Summary

Some people don't want to have kids: Classes meant to be used standalone obey a different blueprint than base classes (see Item 32). Using a standalone class as a base is a serious design error and should be avoided. To add behavior, prefer to add nonmember functions instead of member functions (see Item 44). To add state, prefer composition instead of inheritance (see Item 34). Avoid inheriting from concrete base classes.

### Discussion

Using inheritance when it is not needed betrays a misplaced faith in the power of object orientation. In C++, you need to do specific things when defining base classes (see also Items 32, 50, and 54), and very different and often contrary things when designing standalone classes. Inheriting from a standalone class opens your code to a host of problems, very few of which will ever be flagged by your compiler.

Beginners sometimes derive from value classes, such as a **string** class (the standard one or another), to "add more functionality." However, defining free (nonmember) functions is vastly superior to creating **super_string** for the following reasons:

- Nonmember functions work well within existing code that already manipulates **strings**. If instead you supply a **super_string**, you force changes throughout your code base to change types and function signatures to **super_string**.
- Interface functions that take a **string** now need to: a) stay away from **super_string**'s added functionality (useless); b) copy their argument to a **super_string** (wasteful); or c) cast the **string** reference to a **super_string** reference (awkward and potentially illegal).
- **super_string**'s member functions don't have any more access to **string**'s internals than nonmember functions because **string** probably doesn't have **protected** members (remember, it wasn't meant to be derived from in the first place).
- If **super_string** hides some of **string**'s functions (and redefining a nonvirtual function in a derived class is not overriding, it's just hiding), that could cause widespread confusion in code that manipulates **strings** that started their life converted automatically from **super_string**s.

So, prefer to add functionality via new nonmember functions (see Item 44). To avoid name lookup problems, make sure you put them in the same namespace as the type they are meant to extend (see Item 57). Some people dislike nonmember functions because the invocation syntax is **Fun(str)** instead of **str.Fun()**, but this is just a matter
