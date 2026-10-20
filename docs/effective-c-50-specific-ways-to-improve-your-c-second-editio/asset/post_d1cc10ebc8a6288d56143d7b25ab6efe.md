
// Version two:
try
{
    MyType t1;
    t1 = (MyType)o; // Fails. o is not MyType
    // work with t1, it's a MyType.
}
catch (InvalidCastException)
{
    // report the conversion failure.
}

Both versions fail. But I told you that casts will perform user-defined conversions. You’d think the cast would succeed. You’re right—it should succeed if you think that way. But it fails because your compiler is generating code based on the compile-time type of the object, o. The compiler knows nothing about the runtime type of o; it views o as an instance of object. The compiler sees that there is no user-defined conversion from object to MyType. It checks the definitions of object and MyType. Lacking any user-defined conversion, the compiler generates the code to examine the runtime type of o and checks whether that type is a MyType. Because o is a SecondType object, that fails. The compiler does not check to see whether the actual runtime type of o can be converted to a MyType object.

You could make the conversion from SecondType to MyType succeed if you wrote the code snippet like this:

```
object o = Factory.GetObject();
```

```
// Version three:
SecondType st = o as SecondType;
try
{
    MyType t;
    t = (MyType)st;
    // work with T, it's a MyType.
}
catch (InvalidCastException)
{
    // report the failure.
}
```

You should never write this ugly code, but it does illustrate a common problem. Although you would never write this, you can use an object parameter to a function that expects the proper conversions:

```
```csharp
object o = Factory.GetObject();
DoStuffWithObject(o);
```
```

```
```csharp
private static void DoStuffWithObject(object o)
{
    try
    {
        MyType t;
        t = (MyType)o; // Fails. o is not MyType
        // work with T, it's a MyType.
    }
    catch (InvalidCastException)
    {
        // report the conversion failure.
    }
}
```
```

Remember that user-defined conversion operators operate only on the compile-time type of an object, not on the runtime type. It does not matter that a conversion between the runtime type of o and MyType exists. The compiler just doesn’t know or care. This statement has different behavior, depending on the declared type of st:

```
```csharp
t = (MyType)st;
```
```

This next statement returns the same result, no matter what the declared type of st is. So, you should prefer as to casts—it’s more consistent. In fact, if the types are not related by inheritance, but a user-defined conversion operator exists, the following statement will generate a compiler error:

```
```csharp
t = st as MyType;
```
```

Now that you know to use as when possible, let’s discuss when you can’t use it. The as operator does not work on value types. This statement won’t compile:

```
```csharp
object o = Factory.GetValue();
int i = o as int; // Does not compile.
```
```

That’s because ints are value types and can never be null. What value of int should be stored in i if o is not an integer? Any value you pick might also be a valid integer. Therefore, as can’t be used. You’re stuck using the cast syntax. It’s actually a boxing/unboxing conversion (see Item 45):

```
object o = Factory.GetValue();
int i = 0;
try
{
    i = (int)o;
}
catch (InvalidCastException)
{
    i = 0;
}
```

Using exceptions as a flow control mechanism should strike you as a terrible practice. (See Item 47.) But you’re not stuck with the behaviors of casts. You can use the is statement to remove the chance of exceptions or conversions:

```
object o = Factory.GetValue();
int i = 0;
if (o is int)
    i = (int)o;
```

If o is some other type that can be converted to an int, such as a double, the is operator returns false. The is operator always returns false for null arguments.

The is operator should be used only when you cannot convert the type using as. Otherwise, it’s simply redundant:

```
// correct, but redundant:
object o = Factory.GetObject();

MyType t = null;
if (o is MyType)
    t = o as MyType;
```

The previous code is the same as if you had written the following:

```
// correct, but redundant:
object o = Factory.GetObject();
```

```
MyType t = null;
if (o is MyType)
    t = o as MyType;
```

That’s inefficient and redundant. If you’re about to convert a type using as, the is check is simply not necessary. Check the return from as against null; it’s simpler.

Now that you know the difference among is, as, and casts, which operator do you suppose the foreach loop uses? Foreach loops can operate on nongeneric IEnumerable sequences and have the type coercion built into the iteration. (You should prefer the type-safe generic versions whenever possible. The nongeneric version exists for historical purposes, and to support some late binding scenarios.)

```
public void UseCollection(IEnumerable theCollection)
{
    foreach (MyType t in theCollection)
        t.DoStuff();
}
```

foreach uses a cast operation to perform conversions from an object to the type used in the loop. The code generated by the foreach statement roughly equates to this hand-coded version:

```
public void UseCollectionV2(IEnumerable theCollection)
{
    IEnumerator it = theCollection.GetEnumerator();
    while (it.MoveNext())
    {
        MyType t = (MyType)it.Current;
        t.DoStuff();
    }
}
```

foreach needs to use casts to support both value types and reference types. By choosing the cast operator, the foreach statement exhibits the same behavior, no matter what the destination type is. However, because a cast is used, foreach loops can cause an InvalidCastException to be thrown.

Because IEnumerator.Current returns a System.Object, which has no conversion operators, none is eligible for this test. A collection of SecondType objects cannot be used in the previous UseCollection() function because

the conversion fails, as you already saw. The foreach statement (which uses a cast) does not examine the casts that are available in the runtime type of the objects in the collection. It examines only the conversions available in the System.Object class (the type returned by IEnumerator.Current) and the declared type of the loop variable (in this case, MyType).

Finally, sometimes you want to know the exact type of an object, not just whether the current type can be converted to a target type. The is operator returns true for any type derived from the target type. The GetType() method gets the runtime type of an object. It is a more strict test than the is or as statement provides. GetType() returns the type of the object and can be compared to a specific type.

Consider this function again:

```
public void UseCollectionV3(IEnumerable theCollection)
{
    foreach (MyType t in theCollection)
        t.DoStuff();
}
```

If you made a NewType class derived from MyType, a collection of NewType objects would work just fine in the UseCollection function:

```
public class NewType : MyType
{
    // contents elided.
}
```

If you mean to write a function that works with all objects that are instances of MyType, that’s fine. If you mean to write a function that works only with MyType objects exactly, you should use the exact type for comparison. Here, you would do that inside the foreach loop. The most common time when the exact runtime type is important is when doing equality tests (see Item 6). In most other comparisons, the .isinst comparisons provided by as and is are semantically correct.

The .NET Base Class Library (BCL) contains a method for converting elements in a sequence using the same type of operations: Enumerable.Cast<T>() converts each element in a sequence that supports the classic IEnumerable interface:

```
IEnumerable collection = new List<int>()
    {1,2,3,4,5,6,7,8,9,10};
```

```
var small = from int item in collection
    where item < 5
    select item;
```

```
var small2 = collection.Cast<int>().Where(item => item < 5).
    Select(n => n);
```

The query generates the same method calls as the last line of code above. In both cases, the Cast<T> method converts each item in the sequence to the target type. The Enumerable.Cast<T> method uses an old style cast rather than the as operator. Using the old style cast means that Cast<T> does not need to have a class constraint. Using the as operator would be limiting, and rather than implement different Cast<T> methods, the BCL team chose to create a single method using the old style cast operator. It’s a tradeoff you should consider in your code as well. On those occasions where you need to convert an object that is one of the generic type parameters, you’ll need to weigh the necessity of a class constraint against the different behavior of using the cast operator.

In C# 4.0, the type system can be circumvented even more by using dynamic and runtime type checking. That’s the subject of Chapter 5, “Dynamic Programming in C#.” There are quite a few ways to treat objects based on expectations of known behavior rather than knowing anything about a particular type or interface supplied. You’ll learn about when to use those techniques and when to avoid them.

Good object-oriented practice says that you should avoid converting types, but sometimes there are no alternatives. If you can’t avoid the conversions, use the language’s as and is operators to express your intent more clearly. Different ways of coercing types have different rules. The is and as operators are almost always the correct semantics, and they succeed only when the object being tested is the correct type. Prefer those statements to cast operators, which can have unintended side effects and succeed or fail when you least expect it.

## Item 4: Use Conditional Attributes Instead of #if

#if/#endif blocks have been used to produce different builds from the same source, most often debug and release variants. But these have never been a tool we were happy to use. #if/#endif blocks are too easily abused, creating code that is hard to understand and harder to debug. Language
