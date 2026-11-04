For example, to turn a string into a byte sequence representation for a given encoding scheme, the GetBytes method can be used. In the opposite direction, a byte array can be passed to the GetString method to obtain a .NET string representation back:

```
```csharp
var bytes = Encoding.ASCII.GetBytes("Hello ASCII!");
var hello = Encoding.ASCII.GetString(bytes);
Console.WriteLine(hello);
```
```

This trivial piece of code shows the round-tripping of a simple string through the ASCII encoding scheme. For more complicated examples, refer to MSDN. The fact that some people have made a living out of the creation of text stacks and all the intricacies is good evidence of the depth of the topic. (I have seen plenty of text specialists within Microsoft using Unicode books for their monitor stands.)

# Summary

This chapter introduced essential capabilities offered by the BCL that ships with the .NET Framework. This includes working with various primitive types, ranging from numerical representations, dates, times and GUIDs, all the way to text. Because the BCL is a huge collection of useful tools, it should come as no surprise that chapters covering the BCL's features feel a bit like potpourri. Nonetheless, we've tried hard to keep this chapter related to working with simple data values and objects.

In the next chapters, we explore other facilities of the BCL, including diagnostics and quality assurance for code, I/O mechanisms, and more.