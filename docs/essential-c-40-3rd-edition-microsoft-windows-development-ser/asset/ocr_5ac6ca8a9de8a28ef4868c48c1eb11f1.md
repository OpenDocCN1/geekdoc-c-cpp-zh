```
```
63 65 70 74 69 6F 6E 54 68 72 6F 77 73 . ) // ceptionThrows.
.hash algorithm 0x00008004
.ver 0:0:0:0
}
// module HelloWorld.exe
// MVID {1C349501-2133-A1D6-A82B-B4731061F3F8}
.imagebase 0x00400000
.file alignment 0x00000200
.stackreserve 0x00100000
.subsystem 0x0003 // WINDOWS_CUI
.corflags 0x00000001 // ILONLY
// Image base: 0x00160000
```
```

```
```
// =========================================================
// CLASS MEMBERS DECLARATION
// =========================================================
.class private auto ansi beforefieldinit HelloWorld
extends [mscorlib]System.Object
{
.method private hidebysig static void Main() cil managed
{
.entrypoint
// Code size 13 (0xd)
.maxstack 8
.locals init (
IL_0000: nop
IL_0001: ldstr "Hello. My name is Inigo Montoya."
IL_0006: call void [mscorlib]System.Console::WriteLine(string)
IL_000b: nop
IL_000c: ret
} // end of method HelloWorld::Main
.method public hidebysig specialname rtspecialname
instance void .ctor() cil managed
{
// Code size 7 (0x7)
.maxstack 8
IL_0000: ldarg.0
IL_0001: call instance void [mscorlib]System.Object::.ctor()
IL_0006: ret
} // end of method HelloWorld::.ctor
} // end of class HelloWorld
```
```

```
```
// =========================================================
// ***************** DISASSEMBLY COMPLETE ******************
```
```