# Assembly Manifest

An assembly manifest contains metadata pertaining to an assembly. It is due to the assembly manifest that an assembly becomes self-describing in nature. It acts as an interface for the outside world to interact with the assembly. The contents of an assembly manifest contain the following information:

+   - The name of the assembly
+   - The version of the assembly
+   - The strong name attributes, that is public key and digital signature
+   - The list of files belonging to the assembly
+   - Reference information used by the CLR for referencing assembly types
+   - Information pertaining to the other assemblies that are referenced by the current assembly

A programmer can manipulate the information contained in the assembly manifest with the help of assembly attributes, such as AssemblyCultureAttribute and AssemblyVersionAttribute.

You can view the assembly manifest for an assembly with the help of the ILDasm disassembler tool. Figure D.1 shows a sample assembly manifest:

![](bbox=[0.12, 0.365, 0.865, 0.715])

# Types of Assemblies

The various types of assemblies are the following:

+   - Multi-module Assembly As the name suggests, a multi-module assembly comprises of multiple modules contained in different files. The assembly manifest keeps track of the information pertaining to different modules. In addition, each module has a manifest of its own for storing module-specific information. In case of multi-module assemblies, the assembly manifest may exist either independently in a separate file or inside one of the modules.