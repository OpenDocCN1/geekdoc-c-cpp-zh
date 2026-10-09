```
C# Code

```csharp
class HelloWorld
{
    static void Main()
    {
        System.Console.WriteLine(
            "Hello. My name is Inigo Montoya");
    }
}
```
```

![](bbox=[0.43, 0.26, 0.56, 0.29])

```
CIL Code

```
.method private hidebysig static void Main() cil managed
{
    .entrypoint
    //Code size 11 (0xb)
    .maxstack 8
    IL_0000: ldstr "Hello. My name is Inigo Montoya"
    IL_0005: call void
        [mscorlib]System.Console::WriteLine(string)
    IL_000a: ret
} // end of method HelloWorld::Main
```
```

![](bbox=[0.43, 0.53, 0.56, 0.56])

```
Machine Code

```
00000000 push ebp
00000001 mov ebp,esp
00000003 sub esp,28h
00000006 mov dword ptr [ebp-4],0
0000000d mov dword ptr [ebp-0Ch],0
00000014 cmp dword ptr ds:[001833E0h],0
0000001b je 00000022
0000001d call 75F9C9E0
00000022 mov ecx,dword ptr ds:[01C31418h]
00000028 call dword ptr ds:[03C8E854h]
0000002e nop
0000002f mov esp,ebp
00000031 pop ebp
00000032 ret
```
```

# FIGURE 22.1: Compiling C# to Machine Code