+   - Constructs/initializes parameter arrays
+   - Binds to members of dynamic variables and expressions
+   - Binds to extension methods
+   - Binds/invokes overloaded operators
+   - Constructs delegate objects
+   - Infers types when calling generic methods, declaring a local variable, and using a lambda expression
+   - Defines/constructs closure classes for lambda expressions and iterators
+   - Defines/constructs/initializes anonymous types and instances of them
+   - Rewrites code to support Language Integrated Queries (LINQs; query expressions and expression trees)

And, the CLR itself does all kinds of great things for developers to make our lives even easier. For example, the CLR implicitly:

+   - Invokes virtual methods and interface methods
+   - Loads assemblies and JIT-compiles methods which can potentially throw FileLoadException, BadImageFormatException, InvalidProgramException, FieldAccessException, MethodAccessException, MissingFieldException, MissingMethodException, and VerificationException
+   - Transitions across AppDomain boundaries when accessing an object of a MarshalByRefObject-derived type which can potentially throw AppDomainUnloadedException
+   - Serializes and deserializes objects when crossing an AppDomain boundary
+   - Causes thread(s) to throw a ThreadAbortException when Thread.Abort or AppDomain.Unload is called
+   - Invokes Finalize methods after a garbage collection before objects have their memory reclaimed
+   - Creates type objects in the loader heap when using generic types
+   - Invokes a type’s static constructor potential throwing TypeInitializationException
+   - Throws various exceptions, including OutOfMemoryException, DivideByZeroException, NullReferenceException, RuntimeWrappedException, TargetInvocationException, OverflowException, NotFiniteNumberException, ArrayTypeMismatchException, DataMisalignedException, IndexOutOfRangeException, InvalidCastException