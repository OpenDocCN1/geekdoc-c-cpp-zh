# /keyfile

Similar to the /keycontainer option, the /key option causes the compiler to place a public key into the component’s assembly manifest while signing the assembly with a private key. Use this as follows:

```
vbc.exe MyModule.vb /key:myKey1.sn
```

If your key has a name that includes a space, then you must place quotes around the value as shown here:

```
vbc.exe MyModule.vb /key:"my Key1.sn"
```

# /libpath

When making references to other assemblies while using the /reference compiler option (described earlier), you will not always have these referenced assemblies in the same location as the object being compiled. You can use the /libpath option to specify the location of the referenced assemblies, as illustrated here:

```
vbc.exe MyModule.vb /reference:MyAssembly.dll /libpath:c:\Reuters\bin
```

If you want the compiler to search for the referenced DLLs in more than one location, then specify multiple locations using the /libpath option by separating the locations with a semi-colon:

```
vbc.exe MyModule.vb /reference:MyAssembly.dll /libpath:c:\Reuters\bin, c:\
```

This command means that the compiler will look for the MyAssembly.dll in both the C:\Reuters\bin directory and the root directory found at C:\.

# /main

Using the /main or /m option, you can point the compiler to the class or module that contains the Sub Main procedure. Use it as follows:

```
vbc.exe MyClass.vb /main:MyClass.vb
```

# /moduleassemblyname

This option specifies the name of the assembly the module will be a part of.

# /netcf

This option cannot be executed from Visual Studio itself, but you can use this flag from the Visual Basic command-line compiler. Using /netcf causes the compiler to build your application so that the result is targeted for the .NET Compact Framework, not the full .NET Framework itself. To accomplish this, use the following construct:

```
vbc.exe MyModule.vb /netcf
```

# /nostdlib

By default, the Visual Basic compiler uses standard libraries (System.dll) and the vbc.rsp resource file in the compilation process. Using the /nostdlib option tells the compiler not to use this file in the compilation process, as shown here:

```
vbc.exe MyClass.vb /nostdlib
```

# /platform

The /platform option enables you to specify the platform the compilation should be geared for. Possible options include the following:

+   > /platform:x86 — Compiles the program for an x86 system
+   > /platform:x64 — Compiles the program for a 64-bit system