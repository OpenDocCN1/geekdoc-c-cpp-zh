> As stated, in many programming languages like Java or Python, you do not have much choice. The choice in C# is the power. And, as you know, *with great power comes great responsibility.* ☺

Unlike in languages that support pointers, normally, in C#, the values of a value type follow value semantics, and the values of a reference type, or references, follow reference semantics.

C# provides a way to use reference semantics for values in certain situations. The *ref* keyword (and its two siblings) can be used when a value is passed to a method as an argument, or when a value is returned from a method. Here’s an example:

```
var c = 10;
MultiplyByTwo(ref c);
Console.WriteLine($"c = {c}");

static void MultiplyByTwo(ref int c) {
   c *= 2;
}
```

The output of this program is c = 20.

It is as if a (one-element) array has been created that contains c, and that array is used to call MultiplyByTwo(), as in the previous example using AddOneToElements(). That is reference semantics. Although int is a value type, and c in this case is a value, C# allows us to use reference semantics when needed/desired in certain situations. (This is sometimes called "call by reference" as opposed to "call by value.")

> Note that C#s ref return effectively provides "move semantics". As stated, copying (large) values can be expensive, and in, ref, and out essentially provides a workaround.

On the flip side, if you want to use value semantics for references, then the