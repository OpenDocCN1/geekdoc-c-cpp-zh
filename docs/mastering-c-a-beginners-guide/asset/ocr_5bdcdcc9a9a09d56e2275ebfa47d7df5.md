+   - **Fields.**
+   - **Properties.**
+   - **Methods.**
+   - **Events.**

Late bindings can also be attained through Reflection. To elaborate, you are not able to the idea of which assembly to load during compile time. In this circumstance, you can ask the user to enter the assembly name and Type during the run time, so the application can load the appropriate assembly. With the System.Reflection.Assembly type, you can make available three static types that let you load an assembly directly:

+   1. LoadFrom.
+   2. LoadFrom.
+   3. LoadWithPartialName.

When you contemplate that an assembly is a logical DLL or EXE and a manifest is a comprehensive overview of an assembly, then it is the rationale that a portable executable (PE) file for CTS would have the extension of .dll or .exe. Within the PE file is mostly metadata, which includes a variety of multiple tables:

+   - Method definition table.
+   - Filed definition table.
+   - Type definition table.