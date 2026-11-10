# Survival of Stack Objects

When a procedure is called, a local variable *v*, whose object is allocated on the stack, may have pointers to *v* placed in nonlocal variables. These pointers will continue to exist after the procedure returns, yet the space for *v* disappears, resulting in a dangling-reference situation. Should we ever allocate a local like *v* on the stack, as C does for example? The answer is that the semantics of many languages *requires* that local variables cease to exist when their procedure returns. Retaining a reference to such a variable is a programming error, and the compiler is not required to fix the bug in the program.

to the first approach. We maintain a count of the references to an object, as the mutator performs actions that may change the set of reachable objects. When the count goes to zero, the object becomes unreachable. We discuss this approach in more detail in Section 7.5.3.

The second approach computes reachability by tracing all the references transitively. A *trace-based* garbage collector starts by labeling (“marking”) all objects in the root set as “reachable,” examines iteratively all the references in reachable objects to find more reachable objects, and labels them as such. This approach must trace all the references before it can determine any object to be unreachable. But once the reachable set is computed, it can find many unreachable objects all at once and locate a good deal of free storage at the same time. Because all the references must be analyzed at the same time, we have an option to relocate the reachable objects and thereby reduce fragmentation. There are many different trace-based algorithms, and we discuss the options in Sections 7.6 and 7.7.1.

# 7.5.3  Reference Counting Garbage Collectors

We now consider a simple, although imperfect, garbage collector, based on reference counting, which identifies garbage as an object changes from being reachable to unreachable; the object can be deleted when its count drops to zero. With a reference-counting garbage collector, every object must have a field for the reference count. Reference counts can be maintained as follows:

+   1. *Object Allocation.* The reference count of the new object is set to 1.
+   
+   2. *Parameter Passing.* The reference count of each object passed into a procedure is incremented.
+   
+   3. *Reference Assignments.* For statement `u = v`, where *u* and *v* are references, the reference count of the object referred to by *v* goes up by one, and the count for the old object referred to by *u* goes down by one.