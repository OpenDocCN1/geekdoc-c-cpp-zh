```
```csharp
5  class StringBuilderConstructor
6  {
7      static void Main()
8      {
9          var buffer1 = new StringBuilder();
10         var buffer2 = new StringBuilder(10);
11         var buffer3 = new StringBuilder("hello");
12
13         Console.WriteLine($"buffer1 = \"{buffer1}\"");
14         Console.WriteLine($"buffer2 = \"{buffer2}\"");
15         Console.WriteLine($"buffer3 = \"{buffer3}\"");
16     }
17 }
18
```
```

```
```text
buffer1 = ""
buffer2 = ""
buffer3 = "hello"
```
```

**Fig. 16.9** | Demonstrating StringBuilder class constructors. (Part 2 of 2.)

# 16.11 Length and Capacity Properties, EnsureCapacity Method and Indexer of Class StringBuilder

Class StringBuilder provides the Length and Capacity properties to return the number of characters currently in a StringBuilder and the number of characters that a StringBuilder can store without allocating more memory, respectively. These properties also can be used to increase or decrease the length or the capacity of the StringBuilder. Method EnsureCapacity allows you to reduce the number of times that a StringBuilder's capacity must be increased. The method ensures that the StringBuilder's capacity is at least the specified value. Figure 16.10 demonstrates these methods and properties.

```
```csharp
1  // Fig. 16.10: StringBuilderFeatures.cs
2  // StringBuilder size manipulation.
3  using System;
4  using System.Text;
5
6  class StringBuilderFeatures
7  {
8      static void Main()
9      {
10         var buffer = new StringBuilder("Hello, how are you?");
11
12         // use Length and Capacity properties
13         Console.WriteLine($"buffer = {buffer}" +
14             $"\nLength = {buffer.Length}" +
15             $"\nCapacity = {buffer.Capacity}");
```
```

**Fig. 16.10** | StringBuilder size manipulation. (Part 1 of 2.)