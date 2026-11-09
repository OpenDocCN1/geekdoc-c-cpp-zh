Here the first line builds the `Program.cs` file into a `Program.netmodule` file. The second line produces a small `Program.exe` PE file that contains the manifest metadata tables. In addition, there is a small global function named `__EntryPoint` that is emitted by AL.exe because of the `/main:Program.Main` command-line switch. This function, `__EntryPoint`, contains the following IL code:

```
.method privatescope static void __EntryPoint$PST06000001() cil managed
{
  .entrypoint
  // Code size       8 (0x8)
  .maxstack  8
  IL_0000:  tail.
  IL_0002:  call       void [.module 'Program.netmodule']Program::Main()
  IL_0007:  ret
} // end of method 'Global Functions'::__EntryPoint
```

As you can see, this code simply calls the `Main` method contained in the `Program` type defined in the `Program.netmodule` file. The `/main` switch in AL.exe isn't that useful because it's unlikely that you'd ever create an assembly for an application that didn't have its entry point in the PE file that contains the manifest metadata tables. I mention the switch here only to make you aware of its existence.

With the code that accompanies this book, I have created a Ch02-3-BuildMultiFileLibrary.bat file that encapsulates all the steps required to build a multifile assembly. The Ch02-4-AppUsingMultiFileLibrary project in Visual Studio invokes this batch file as a prebuild command-line step. You can examine this project to see how to integrate building and referencing a multifile assembly from within Visual Studio.

# ## Adding Resource Files to an Assembly

When using AL.exe to create an assembly, you can add a file as a resource to the assembly by using the `/embed[resource]` switch. This switch takes a file (any file) and embeds the file's contents into the resulting PE file. The manifest's `ManifestResourceDef` table is updated to reflect the existence of the resources.

AL.exe also supports a `/link[resource]` switch, which also takes a file containing resources. However, the `/link[resource]` switch updates the manifest's `ManifestResourceDef` and `FileDef` tables, indicating that the resource exists and identifying which of the assembly's files contains it. The resource file is not embedded into the assembly PE file; it remains separate and must be packaged and deployed with the other assembly files.

Like AL.exe, CSC.exe also allows you to combine resources into an assembly produced by the C# compiler. The C# compiler's `/resource` switch embeds the specified resource file into the resulting assembly PE file, updating the `ManifestResourceDef` table. The compiler's `/linkresource` switch adds an entry to the `ManifestResourceDef` and the `FileDef` manifest tables to refer to a stand-alone resource file.