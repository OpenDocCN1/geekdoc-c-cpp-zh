Another complexity comes from the way the C# grammar was written in the first place. It was originally assumed that all reference variables were potentially nullable.

For example, one will have to use certain "nullable attributes" when calling a function with a reference type argument, sometimes *before* and *after*. That is well beyond the scope of this book, however.

When in doubt, you should fall back to the old behavior. Assume that a reference variable can be null unless you are absolutely sure that it cannot be null. Clearly, using nullable reference variables for *all* reference variables (within the enabled nullable context) beats the purpose. Some efforts will need to be made to reduce the number of nullable reference variables.

Despite all these issues, we will use the enabled nullable context in this book, across all the examples. As stated, this could be the way we program in C#, in the not-so-distant future.

The best approach is to start using the enabled nullable context but use primarily nullable reference variables just as you have been, and to gradually decrease the use of the nullable reference variables, over time, as just stated.

> The nullable context is relevant only to the reference variables, in certain situations. Even though we use the enabled nullable context in all the examples in this book, it may not always be relevant, or even apparent. And, in many cases, it is not really visible because we cannot see what is not there. The sample code in this book mostly lack the (rather common, in fact ubiquitous) null check if statements.

You can enable the nullable context using the C# compile time directives. To enable, put this is in your source code file:

```
#nullable enable
```