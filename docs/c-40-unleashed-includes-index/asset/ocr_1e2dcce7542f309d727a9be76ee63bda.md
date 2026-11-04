```
CallConvtn: [DEFAULT]
hasThis
ReturnType: I4
2 Arguments
    Argument #1: I4
    Argument #2: I4
2 Parameters
    (1) ParamToken : (08000001)
        Name : a
        flags: [none] (00000000)
    (2) ParamToken : (08000002)
        Name : b
        flags: [none] (00000000)

Method #2 (06000003)
--------------------------------------------------
MethodName: .ctor (06000003)
Flags      : [Public] [HideBySig] [ReuseSlot] [SpecialName]
            [RTSpecialName] [.ctor]   (00001886)
RVA        : 0x000020a3
ImplFlags  : [IL] [Managed]   (00000000)
CallConvtn: [DEFAULT]
hasThis
ReturnType: Void
No arguments.
```

Here, you can observe the names of types and members associated with several flags (for things such as visibility, method table layouts, and so forth). In addition, notice that every piece of metadata has a unique number that allows for other pieces of metadata to cross-reference it.

# Mixing Languages

In the previous discussion, you’ve seen how to use a single language, in our case C#, to build a complete application. This seldom is the case in a real-world environment where libraries from various sources need to be combined to provide an end-to-end solution to the problem at hand. In fact, our use of BCL types like System.Random and System.Console is a good example of such a scenario. Although those happen to be written in C# too, as most of the code in BCL is, that’s not a requirement at all thanks to the cross-language capabilities provided by the CLR. However, consuming libraries is just the tip of the language interoperability iceberg. Richer capabilities, such as extending existing types in a different language than they were initially written in, is also part of the picture.

Let’s explore this angle to the CLR in a more concrete fashion. Instead of compiling our Calculator class as part of an executable assembly, we’ll compile it into a library with a .dll extension. As a matter of fact, the runtime cares little about the file extension to an assembly, apart from the fact that EXE files are supposed to have an entry-point method.