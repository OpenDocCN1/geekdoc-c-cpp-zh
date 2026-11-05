Follow these steps to create and call a .NET assembly with Visual Studio 2008 :

# Create the Assembly :

+   1. Select File " New " Project from the menu.
+   2. Select Class Library from the template menu.
+   3. Type the required code in the .vb file :
+   4. Select Build Solution from the Build menu.
+   5. Once the DLL is created, copy and paste it in the C:\ directory.

# Call the Assembly :

+   1. Select File " New " Project from the menu.
+   2. Select Console Application from the template menu.
+   3. Type the required code in the .vb file :
+   4. Now the code can be built and executed.

# Q.11 Recall private and shared assemblies.

Ans. : The terms 'private' and 'shared' refer to how an assembly is deployed and not any intrinsic attributes of the assembly. A private assembly is normally used by a single application, and is stored in the application's directory, or a sub-directory beneath. A shared assembly is intended to be used by multiple applications, and is normally stored in the Global Assembly Cache (GAC), which is a central repository for assemblies. A Strong name has to be created for public assembly while strong name is not required for private assembly. Moreover, private assembly doesn't have any version constraint on the other hand public assembly should strictly enforce version constraint.

# Private Assembly

+   - This type of assembly is used by a single application. It is stored in the application's directory or the applications sub-directory. There is no version constraint in a private assembly.
+   - Shared Assembly or Public Assembly
+   - A shared assembly has version constraint. It is stored in the Global Assembly Cache (GAC). GAC is a repository of shared assemblies maintained by the .NET runtime. It is located at C:\Windows\Assembly OR C:\Winnt\Assembly. The shared assemblies may be used by many applications. To make an assembly a shared assembly, it has to be strongly named. In order to share an assembly with many applications, it must have a strong name.