# ### ✓ Checkpoint

+   1. *(True/False)* A class’s destructor is called implicitly when an object is destroyed, typically when program control leaves the scope in which that object was created.  
+      **Answer:** True.

+   2. *(Fill-in)* Every class has one destructor. If you do not explicitly define one, the compiler defines a ________ destructor that invokes any class-type data members’ destructors.  
+      **Answer:** default.

# ## 9.13 When Constructors and Destructors Are Called

The order in which constructors and destructors are called depends on the objects’ scopes. Generally, destructor calls are made in the reverse order of the corresponding constructor calls, but as we’ll see in Figs. 9.13–9.15, global and static objects can alter the order in which destructors are called.

# ### Constructors and Destructors for Objects in Global Scope

Constructors are called for objects defined in the global scope (also called global namespace scope) before executing any other function in that file. The execution order of global object constructors among multiple files is not guaranteed, so global objects in separate files should not depend on one another. When `main` terminates via a `return` statement or by reaching its closing brace, the corresponding destructors are called in the reverse order of their construction.

# ### Destructors on Program Termination

The `exit` function often is called to terminate a program immediately when a fatal unrecoverable error occurs. In this case, the destructors of local objects do not execute.^28 Function `abort` performs similarly to function `exit` but forces the program to terminate immediately without allowing programmer-defined cleanup code of any kind to be called.

Function `abort` is usually used to indicate abnormal program termination.^29

# ### Constructors and Destructors for Non-static Local Objects

A non-static local object’s constructor is called when execution reaches the object’s definition. Its destructor is called when execution leaves the object’s scope—that is, when the block in which that object is defined finishes executing normally or due to an exception. Destructors are not called for local objects if the program terminates with a call to function `exit` or `abort`.

# ### Constructors and Destructors for static Local Objects

The constructor for a static local object is called only once when execution first reaches the point where the object is defined. The corresponding destructor is called when `main` terminates or the program calls function `exit`. Global and static objects are destroyed in