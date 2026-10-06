do
regexTy.AddMember ctor
providedMethods |> Seq.iter regexTy.AddMember

do this.Namespace(rootnamespace, [regexTy])

[<TypeProviderAssembly>
do ()

# LISTING 5-31 IL code from the compiled binary reference to the type provider

```
IL_0000: nop
IL_0001: newobj instance void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2::ctor()
IL_0006: box [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2
IL_0008: unbox. [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2
IL_0009: dup
IL_0011: stfld class
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2 '<StartupClassCons
leApplication1>$Program'::$08
IL_0016: stloc.0
IL_0017: call class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.
BaseType2.
Program::get_t()
IL_001c: ldr "F1"
IL_0021: call void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.InsertFunctions::LogBeforeEx
ecution(class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2,
string)
IL_0026: call class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.
BaseType2
Program::get_t()
IL_002b: ldr "hello"
IL_0030: callvirt instance void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2::$F1(string)
IL_0035: call class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.
BaseType2
Program::get_t()
IL_003a: ldr "F1"
IL_003f: call void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.InsertFunctions::LogAfterExe
cution(class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2,
string)
IL_0044: call class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.
BaseType2
Program::get_t()
IL_0049: ldr "F2"
```