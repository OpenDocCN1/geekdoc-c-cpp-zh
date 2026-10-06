# 26 CHAPTER 2 INTRODUCING LINQ TO OBJECTS

you would need to define a concrete type for each and every return set that altered the columns of interest. Optional parameters added in C# 4.0 (covered in Chapter 4, “Grouping and Joining Data”) make this somewhat easier, anonymous types should be considered when results are needed temporarily.

Beyond their usefulness of supporting LINQ, anonymous types allow temporary data structures to be created during processing of that data. It was often necessary to build a plain, old class with nothing more than property declarations to support holding data; anonymous types fulfill the need perfectly. Although it is possible to pass anonymous types beyond the method that declared them by declaring an argument type as Object, this is highly discouraged. When using anonymous types outside of LINQ functionality, keep the scoping to the method they are, otherwise define a concrete type or struct.

# Lambda Expressions

Lambda expressions build upon the anonymous methods feature added in C# 2.0. Anonymous methods added the ability to inline the code by using the delegate keyword, which avoids the need to declare a delegate method in a separate body of code. C# 3.0 introduces the lambda operator =>, which can be used to create delegates or expression trees in an even briefer syntax.

> NOTE Delegate is a fancy term for a type-safe reference (pointer) to a function or method. For example, when you need to call code when someone clicks a button, you actually attach a Delegate to the event. The Delegate is the actual method implementing the code elsewhere. However, having to locate Delegate code separately (such as within a concrete method) was a pain, and in C# 2.0 the ability to inline code was added. In C# 3.0, lambda expressions clean the syntax of writing that in-line code even more.

This C# 2.0 syntax for an anonymous method is

```
delegate (type parameter) {
  [ method body ] return [expression]; }
```

The same delegate using the C# 3.0 lambda expression syntax is

```
[parameter] => [expression]
```