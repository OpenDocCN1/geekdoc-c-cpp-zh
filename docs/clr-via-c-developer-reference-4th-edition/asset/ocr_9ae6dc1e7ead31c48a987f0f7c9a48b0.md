Note If a strongly named assembly is packaged in a cabinet (.cab) file or is compressed in some way, the assembly's file must first be decompressed to temporary file(s) before you use GUtil.exe to install the assembly's files into the GAC. The assembly's files have been installed, the temporary file(s) can be deleted.

The GUtil.exe tool doesn't with the end-user .NET Framework redistribut package. If your application includes some assemblies that you have deployed into the GAC, you should use the Windows Installer (MSI), MSI is the only tool that guaranteed to be on end-user machines and capable of installing assemblies into the GAC.

Important Globally deploying assemblies into the GAC is a form of registering the assembly, although the actual Windows registry isn't affected in any way. Installing assemblies into the GAC breaks the goal of simple application installation, backup, restore, moving, and uninstall. So it is recommended that you avoid global deployment and use private deployment whenever possible.

What is the purpose of “registering” an assembly in the GAC? Well, say two companies produce OurLibrary assembly consisting of one file: OurLibrary.dll. Obviously, both of these files go in the same directory because the last one installed would overwrite the first one, breaking some application. When you install an assembly in the GAC, dedicated subdirectories are created under the %SystemRoot%Microsoft.NET\Assembly directory, and the assembly files are copied into one of these subdirectories.

Normally, one examines the GAC's subdirectories, so the structure of the GAC shouldn't really matter to you. As long as the tools and the CLR know the structure, all is good.

# Building an Assembly That References a Strongly Named Assembly

Whenever you build an assembly, the assembly will have references to other strongly named assemblies. This is true because System.Object is defined in MSCorLib.dll, which is strongly named. However, it's likely that an assembly will reference types other strongly named assemblies published by either Microsoft, a third party, or your own organization. In Chapter 2, I showed you how to use CSC.exe's /reference compiler switch to specify the assembly file names what to reference. If the file name is a full path, CSC.exe loads the specified file and its metadata information to build the assembly. As mentioned in Chapter 2, if you specify a file without a path, CSC.exe attempts to find the assembly by looking in the following directories (in order of their presentation here):

+   1. Working directory.

+   2. The directory that contains the CSC.exe file itself. This directory also contains the CLR DLLs.