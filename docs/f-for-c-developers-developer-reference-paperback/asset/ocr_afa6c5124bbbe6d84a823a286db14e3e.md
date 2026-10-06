```
IL_004e: call void
[ShareInfoSampleProvider]Samples.Fshar.ShareInfoProvider.InsertFunctions::LogBeforeEx
cution(class[ShareInfoSampleProvider]Samples.Fshar.ShareInfoProvider.BaseType2,
string)
IL_0053: call class [ShareInfoSampleProvider]Samples.Fshar.ShareInfoProvider.
BaseType2
Program::get_t())
IL_0058: dic.42
IL_0059: callvirt instance void
[ShareInfoSampleProvider]Samples.Fshar.ShareInfoProvider.BaseType2::F2(int32)
IL_005e: call class [ShareInfoSampleProvider]Samples.Fshar.ShareInfoProvider.
BaseType2
Program::get_t())
IL_0063: dstr "F2"
IL_0068: call void
[ShareInfoSampleProvider]Samples.Fshar.ShareInfoProvider.InsertFunctions::LogAfterExe
cution(class[ShareInfoSampleProvider]Samples.Fshar.ShareInfoProvider.BaseType2,
string)
IL_006d: ret
```

At first glance, the wrapper type provider does not appear to derive its type and members from a schema. In this case, the schema is being defined by the data returned from TypeInfo and Method reflection. From this sample, I can say that the base class is another way to get schema data in addition to static type parameters and local files. The type provider has the ability to rearrange the data, which are methods and properties, to its new location and insert customized code during relocation. The next sample shows how to make an inheritance structure with a type provider.

# Using the Multi-Inheritance Type Provider

With C#, the decision was made not to support multi-inheritance. Discussions about the advantages or disadvantages of multi-inheritance often open a can of worms. I am not going to pick a side in this discussion. Instead, this attempt to demonstrate that a type provider can create a new inheritance hierarchy. Because the user has full control over to generate the class members, he can decide how to handle any duplicated function names or other nasty problems. This example uses only unique function names and leaves the duplicated-function-name problem to the reader.

First assume C# classes needs to be handled by the type provider. The C# class definition is presented in Listing 5-32. The C# classes that are sealed make the traditional inheritance more difficult. Note that if the class is located in another assembly, you to make sure that the assembly be found (as shown in Listing 5-33) if the DLL is located next to the type provider DLL.