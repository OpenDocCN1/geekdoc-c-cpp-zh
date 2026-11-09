> > **Important** Globally deploying assembly files into the GAC is a form of registering the assembly, although the actual Windows registry isn't affected in any way. Installing assemblies into the GAC breaks the goal of simple application installation, backup, restore, moving, and uninstall. So it is recommended that you avoid global deployment and use private deployment whenever possible.

What is the purpose of “registering” an assembly in the GAC? Well, say two companies each produce an OurLibrary assembly consisting of one file: OurLibrary.dll. Obviously, both of these files can't go in the same directory because the last one installed would overwrite the first one, surely breaking some application. When you install an assembly into the GAC, dedicated subdirectories are created under the C:\Windows\Assembly directory, and the assembly files are copied into one of these subdirectories.

Normally, no one examines the GAC's subdirectories, so the structure of the GAC shouldn't really matter to you. As long as the tools and the CLR know the structure, all is good.

# # Building an Assembly That References a Strongly Named Assembly

Whenever you build an assembly, the assembly will have references to other strongly named assemblies. This is true because System.Object is defined in MSCorLib.dll, which is strongly named. However, it's likely that an assembly will reference types in other strongly named assemblies published either by Microsoft, a third party, or your own organization. In Chapter 2, I showed you how to use CSC.exe's /reference compiler switch to specify the assembly file names you want to reference. If the file name is a full path, CSC.exe loads the specified file and uses its metadata information to build the assembly. As mentioned in Chapter 2, if you specify a file name without a path, CSC.exe attempts to find the assembly by looking in the following directories (in order of their presentation here):

+   1. Working directory.
+   2. The directory that contains the CSC.exe file itself. This directory also contains the CLR DLLs.
+   3. Any directories specified using the /lib compiler switch.
+   4. Any directories specified using the LIB environment variable.

So if you're building an assembly that references Microsoft's System.Drawing.dll, you can specify the /reference:System.Drawing.dll switch when invoking CSC.exe. The compiler will examine the directories shown earlier and will find the System.Drawing.dll file in the directory that contains the CSC.exe file itself, which is the same directory that contains the DLLs for the version of the CLR the compiler is tied to. Even though this is the directory where the assembly is found at compile time, this isn't the directory where the assembly will be loaded from at runtime.