The following code demonstrates string interning.

```
```csharp
String s1 = "Hello";
String s2 = "Hello";
Console.WriteLine(Object.ReferenceEquals(s1, s2));   // Should be 'False'

s1 = String.Intern(s1);
s2 = String.Intern(s2);
Console.WriteLine(Object.ReferenceEquals(s1, s2));   // 'True'
```
```

In the first call to the ReferenceEquals method, s1 refers to a "Hello" string object in the heap, and s2 refers to a different "Hello" string object in the heap. Because the references are different, False should be displayed. However, if you run this on version 4.5 of the CLR, you'll see that True is displayed. The reason is because this version of the CLR chooses to ignore the attribute/flag emitted by the C# compiler, and the CLR interns the literal "Hello" string when the assembly is loaded into the AppDomain. This means that s1 and s2 refer to the single "Hello" string in the heap. However, as mentioned previously, you should never write code that relies on this behavior because a future version of the CLR might honor the attribute/flag and not intern the "Hello" string. In fact, version 4.5 of the CLR does honor the attribute/flag when this assembly's code has been compiled using the NGen.exe utility.

Before the second call to the ReferenceEquals method, the "Hello" string has been explicitly interned, and s1 now refers to an interned "Hello". Then by calling Intern again, s2 is set to refer to the same "Hello" string as s1. Now, when ReferenceEquals is called the second time, we are guaranteed to get a result of True regardless of whether the assembly was compiled with the attribute/flag.

So now, let's look at an example to see how you can use string interning to improve performance and reduce memory usage. The NumTimesWordAppearsEquals method below takes two arguments: a word and an array of strings in which each array element refers to a single word. This method then determines how many times the specified word appears in the wordlist and returns this count.

```
```csharp
private static Int32 NumTimesWordAppearsEquals(String word, String[] wordlist) {
    Int32 count = 0;
    for (Int32 wordnum = 0; wordnum < wordlist.Length; wordnum++) {
        if (word.Equals(wordlist[wordnum], StringComparison.Ordinal))
            count++;
    }
    return count;
}
```
```