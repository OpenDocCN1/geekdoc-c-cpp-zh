+   - R.20: Use unique_ptr or shared_ptr to represent ownership.

+   - R.21: Prefer unique_ptr over shared_ptr unless you need to share ownership.

+   - E.6: Use RAII to prevent leaks.

+   - E.13: Never throw while being the direct owner of an object [and thus bypass the intended delete (or other cleanup operations)].

+   - E.16: Destructors, deallocation, and swap (...) must never fail. [So, neither throw an exception nor fail.].

+   - Section C.other mainly deals with value classes. [It explains what you should consider for swap and ==].

# Casting a UML diagram into an implementation not a one-to-one

30.2.4 Class Hierarchies

transformation, even if it is a class diagram. There are implementation details to consider. Conversely, you can represent a given C++ class hierarchy with a UML diagram. Not every method needs to be implemented as a member. An (overloaded?) free function is better suited for extension if you do not need to access the internals of the class.

No, a good class hierarchy is not an easy task. And because software development is a moving target, you must ensure during the design phase that your hierarchy is testable so that you can respond to changes with new extensions and refactoring of existing components. There are also helpful guidelines for this.