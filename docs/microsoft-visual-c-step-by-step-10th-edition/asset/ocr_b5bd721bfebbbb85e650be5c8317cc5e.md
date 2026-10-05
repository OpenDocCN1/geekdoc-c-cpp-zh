- Any parameters (including ref and out keyword modifiers) match exactly.

- All methods implementing an interface must be publicly accessible. However, if you're using an explicit interface implementation, the method shouldn't have an access qualifier.

If there's any difference between the interface definition and its declared implementation, the class will not compile.

> Tip
The Microsoft Visual Studio integrated development environment (IDE) can help reduce coding errors caused by failing to implement the methods in an interface. The Implement Interface wizard can generate stubs for each item in an interface that a class implements. You then fill in these stubs with the appropriate code. You'll see how to use this wizard in the exercises later in this chapter.

A class can inherit from another class and implement an interface at the same time. In this case, C# does not distinguish between the base class and the interface by using specific keywords as, for example, Java does. Instead, C# uses a positional notation. The base class is always named first, followed by a comma, followed by the interface. The following example defines Horse as a class that is Mammal but that additionally implements the IBound interface:

Click here to view code image

```
interface ILandBound{
  ...
}

class Mammal{
  ...
}

class Horse : Mammal , ILandBound
{
```