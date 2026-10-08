# Equivalence in CLR

As discussed, CLR 4.0 supports embedding type information for COM types directly into managed assemblies, instead of obtaining that type information from interoperability assemblies. The compiler generates concise code, and the embedded type information includes only the types and members that are actually used by the managed assembly. Because of this behavior, two assemblies might have very different views of the same COM type. Each assembly has a different System.Type object to represent its view of that COM type.

From the CLR's perspective, type equivalence means a COM object that is passed from one assembly to another can be cast to the appropriate managed type in the receiving assembly.

The CLR supports equivalence only for COM types, and as a limitation, for interfaces, structures, enumerations, and delegates. Classes are not subject to this behavior. Two COM types are taken into account as equivalent ones, where the following criteria are met:

+   - The types are both interfaces or structures or enumerations or delegates.
- Both types are COM import types.
- If they are interfaces, they should be decorated with the ComImportAttribute and GuidAttribute attributes.
- The assemblies in which they are defined (that are generally two separate ones) have either the ImportedFromTypeLibAttribute or the PrimaryInteropAssembly Attribute.
- The GuidAttribute values of these types are equal.

During the build process, the compiler checks if a type is used in a context where type equivalence is assumed. In this case, it checks if the criteria are met. In cases when there are issues, the compiler raises appropriate error messages.

The compiler decodes the type declarations with the TypeIdentifierAttribute and the CompilerGeneratedAttribute attributes.

> As this writing, the Beta 2 version of the .NET Framework and Visual Studio 2010 is active. There are some contradictions between the MSDN documentation and the real operation of type equivalence, mainly about the role of the TypeIdentifierAttribute. The criteria described previously are subject to change. Check the current MSDN documentation for "Type Equivalence and Embedded Interop Types."

# PARALLEL COMPUTING

In the last 15 years, computer CPUs went quite fast, and, according to Moore's law, their computing capacity was doubled every 18 months. This was especially eye-catching for graphics cards and GPUs, where the performance improvements exceeded even Moore's law. For a long time,