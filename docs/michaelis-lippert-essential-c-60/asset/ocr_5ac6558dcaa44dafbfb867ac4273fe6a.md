Regardless of whether a namespace declaration follows the pattern shown in Listing 9.14, that in Listing 9.15, or a combination of the two, the resultant CIL code will be identical. The same namespace may occur multiple times, in multiple files, and even across assemblies. For example, with the convention of one-to-one correlation between files and classes, you can define each class in its own file and surround it with the same namespace declaration.

Given that namespaces are key for organizing types, it is frequently helpful to use the namespace for organizing all the class files. For this reason, it is helpful to create a folder for each namespace, placing a class such as AddisonWesley.Fezzik.Services.Registration into a folder hierarchy corresponding to the name.

When using Visual Studio projects, if the project name is Addison Wesley.Fezzik, you should create one subfolder called Services into which RegistrationService.cs is placed. You would then create another subfolder—Data, for example—into which you place classes relating to entities within the program—RealestateProperty, Buyer, and Seller, for example.

# Guidelines

+   - DO prefix namespace names with a company name to prevent namespaces from different companies having the same name.
+   - DO use a stable, version-independent product name at the second level of a namespace name.
+   - DO NOT define types without placing them into a namespace.
+   - CONSIDER creating a folder structure that matches the namespace hierarchy.

# Namespace Alias Qualifier

Namespaces on their own deal with the vast majority of naming conflicts that might arise. Nevertheless, sometimes (albeit rarely) conflict can arise because of an overlap in the namespace and class names. To account for this possibility, the C# 2.0 compiler includes an option for providing an alias with the /reference option. For example, if the assemblies CoordinatesPlus.dll and Coordinates.dll have an overlapping type of Arc, you can reference both assemblies on the command line by assigning