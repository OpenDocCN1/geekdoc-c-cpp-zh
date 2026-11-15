“references,” and as such, the objects are not garbage until after their finalization methods are called and the object references are removed from the f-reachable queue.

# Language Contrast: C++—Deterministic Destruction

Although finalizers are similar to destructors in C++, the fact that their execution cannot be determined at compile time makes them distinctly different. The garbage collector calls C# finalizers sometimes after they were last used, but before the program shuts down; C++ destructors are automatically called when the object (not a pointer) goes out of scope.

Although running the garbage collector can be a relatively expensive process, the fact that garbage collection is intelligent enough to delay running until process utilization is somewhat reduced offers an advantage over deterministic destructors, which will run at compile-time-defined locations, even when a processor is in high demand.

# ADVANCED TOPIC

# Resurrecting Objects

By the time an object’s finalization method is called, all references to the object have disappeared and the only step before garbage collection is running the finalization code. However, it is possible to add a reference inadvertently for a finalization object back into the root reference’s graph. In so doing, the referenced object is no longer inaccessible, and therefore, it is not ready for garbage collection. However, if the finalization method for the object has already run, it will not necessarily be run again unless it is explicitly marked for finalization (using the GC.ReRegisterFinalize() method).

Obviously, resurrecting objects like this is peculiar behavior and you should generally avoid it. Finalization code should be simple and should focus on cleaning up only the resources that it references.