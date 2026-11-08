+   - A destructor (see Chapter 16) must be virtual if there is at least one virtual method in the class.
+   - A virtual method of a base class that you override is automatically also virtual, even if you don't explicitly say so. Once virtual, always virtual.

> **Classes Either Entirely without or Entirely with “virtual”**
> 
> For starters, I recommend following these two rules:
> 
> - Without a hierarchy, make nothing virtual.
> - With a hierarchy, make *all* methods virtual if you override at least one method.
> 
> If you keep this in mind, you'll likely design your classes (and hierarchies) in a way that naturally leads to the decision of whether a method should be virtual or not.

But why ask the question at all? What are the advantages and disadvantages of virtual methods?

The big advantage is that you gain a more flexible design. You can modify behavior in derived classes even if it was originally defined in a base class.

The disadvantages concern speed and memory:

+   - **The method must first be looked up in a table at runtime.**
+     When you call a virtual method, this call requires one more indirection (and possibly an addition). But modern processors handle this effortlessly, and you will not notice any speed differences compared to a normal method call.
+   - **Virtual methods can rarely be optimized into inline functions.**
+     You might notice this more in the program's speed, especially if you call a virtual function within a tight loop. Inlining is a crucial compiler optimization, and its importance increases with the complexity and modernity of the processor executing the program.
+   - **A hidden data field is required per instance.**
+     Each instance of a class with at least one virtual method has an additional hidden variable. This is implemented in most C++ compilers: it is a pointer (*vptr*) to a static table (*vtable*). If you have small instances that you pack in large quantities—for example, in a container—it will affect memory usage.

You could also argue that you want to align your design with other current programming languages. Java, for example, does not have any nonvirtual methods. I advocate at least separating *data-holding classes* (*data transfer objects* [DTOs]) from *behavior-oriented classes* (with nontrivial methods) in the design. DTOs do not need virtuality, but business logic classes might, depending on the purpose. Someone who decides to make all methods virtual "just to be sure" should consider whether this approach is suitable for their application. While I can understand the reasoning behind this design decision, it's essential to ensure that it is appropriate.