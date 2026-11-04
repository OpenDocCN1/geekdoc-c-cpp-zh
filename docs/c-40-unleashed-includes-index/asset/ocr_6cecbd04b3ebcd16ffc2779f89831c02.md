```
[My("Hello", NamedInt=42)]
class Program
{
    ...
}
```

Looking in ILDASM, the first thing you can see is how the custom attribute is hidden behind some .custom construct, as shown in Figure 21.12.

![](bbox=[0.1, 0.35, 0.78, 0.6])

FIGURE 21.12 A custom attribute showing up in ILDASM.

What you can already see from this is how the custom attribute is represented by a sequence of bytes, which contain the constant data for it. In other words, there's no way a custom attribute can rely on the execution of code to compute its data values because all data is serialized into a byte sequence. You can dig a little deeper and go to View, MetaInfo, Show (Ctrl+M) to show type definitions and such in a textual format. In there, the type definition for Program will reveal the following attribute:

```
TypeDef #2 (02000003)
....................................................
TypDefName: Program  (02000003)
...
CustomAttribute #1 (0c000006)
....................................................
    CustomAttribute Type: 06000001
    CustomAttributeName: MyAttribute :: instance void .ctor(class String)
    Length: 25
    Value : 01 00 05 48 65 6c 6c 6f 01 00 54 08 08 4e 61 6d ...
    ctor args: ("Hello_")
```

# Discovering Custom Attributes

Although most readers will likely just have to use custom attributes to use certain pieces of the framework (like MEF, WCF, and so forth) or to use external libraries, it's useful to know how to declare and discover custom attributes. You've already seen how to declare them, but how can your code now inspect a given assembly, type, or member and figure out whether an attribute is applied? Again, the answer lies in reflection.