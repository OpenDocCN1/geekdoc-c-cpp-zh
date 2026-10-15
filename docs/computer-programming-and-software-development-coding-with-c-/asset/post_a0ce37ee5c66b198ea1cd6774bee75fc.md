
Now, the issue that we have is we want to replace these four occurrences of the double type when the SimpleStack class is used. So, we don't want to hard code the double type into this class. We actually need something like a type placeholder that can be specified when the SimpleStack class is used. So, I replace all these double types with TypePlaceholder. Now, the great thing is you can do exactly this with generics. This is what generics are made for. To define the TypePlaceholder, you add a pair of angle brackets after the class name and then you use the TypePlaceholder name.

![](img/0155736aec718cf18821e9f10a5d308d_1052_0.png)

Now you see the class doesn't have any errors anymore. This is now a generic type parameter that you need to pass to the SimpleStack class when you use the SimpleStack class. But before we use it, I want to tell you a few more things how you should name this TypePlaceholder. You can give it any name you want, but the recommendation is to call this just T, or if you want to specify a more specific name, you can call it, for example, in this case TItem. But as you see, you always start with an uppercase T.

```csharp
public class SimpleStack<T>
{
    private readonly T[] _items;
    private int _currentIndex = -1;

    public SimpleStack() => _items = new T[10];

    public int Count => _currentIndex + 1;

    public void Push(T item) => _items[++_currentIndex] = item;

    public T Pop() => _items[_currentIndex--];
}
```

In this case, I think it's obvious what T is, so let's just call it T. So in the code, instead of TypePlaceholder, I use everywhere just T. But it is a TypePlaceholder for the type that needs to be specified when the SimpleStack class is used. Now you have created a generic SimpleStack class. You read this class name actually as SimpleStack of T. Now, if you use this class, for example, with the type double, all these occurrences will be of type double. If you use it with a type string, all these Ts that you see here will be strings. Now let's go back to the Program.cs file and let's use the generic SimpleStack class.

```csharp
public class SimpleStack
{
    private readonly double[] _items;
    private int _currentIndex = -1;

    public SimpleStack() => _items = new double[10];

    public int Count => _currentIndex + 1;

    public void Push(double item) => _items[++_currentIndex] = item;

    public double Pop() => _items[_currentIndex--];
}
```

So here in the StackDoubles method, let's create a SimpleStack instance and let's add an opening angle bracket to pass the generic type argument to the SimpleStack class. Here, we want to use the SimpleStack class with the type double.

```csharp
public class SimpleStack<TypePlaceholder>
{
    private readonly TypePlaceholder[] _items;
    private int _currentIndex = -1;

    public SimpleStack() => _items = new TypePlaceholder[10];

    public int Count => _currentIndex + 1;

    public void Push(TypePlaceholder item) => _items[++_currentIndex] = item;

    public TypePlaceholder Pop() => _items[_currentIndex--];
}
```

Now as you can see, the code in this StackDoubles method does not have any errors. When you hover the Push method, you can see it takes a double.

```csharp
public class SimpleStack<T>
{
    private readonly T[] _items;
    private int _currentIndex = -1;

    public SimpleStack() => _items = new T[10];

    public int Count => _currentIndex + 1;

    public void Push(T item) => _items[++_currentIndex] = item;

    public T Pop() => _items[_currentIndex--];
}
```

This means no boxing happens and the SimpleStack instance is also type safe. When you try to push, for example, here a Boolean into the SimpleStack of double, then you can see you get the error here, cannot convert from bool to double. So let's remove this again. Also when you hover the Pop method, you can see it returns a double, so everything is typed.

```csharp
private static void StackDoubles()
{
    var stack = new SimpleStack<double>();
    stack.Push(1.2);
    stack.Push(3.4);
    stack.Push(5.6);

    double sum = 0.0;

    while (stack.Count > 0)
    {
        double item = stack.Pop();
        Console.WriteLine($"Item: {item}");
        sum += item;
    }

    Console.WriteLine($"Sum: {sum}");
}
```

Now let's scroll down to the StackStrings method. Here in the StackStrings method, we need a SimpleStack that works with strings. So let's create here a SimpleStack of string. Now when you hover here in this case the Push method, you can see it takes a string. Also, the Pop method returns a string, so everything is type safe.

```csharp
private static void StackDoubles()
{
    var stack = new SimpleStack<double>();
    stack.Push(1.2);
    stack.Push(2.8);
    stack.Push(3.0);
    stack.Push(true);
    double sum = 0;
    while (stack.Count > 0)
    {
        double item = stack.Pop();
        Console.WriteLine($"Item: {item}");
        sum += item;
    }
}

readonly struct System.Boolean
Represents a Boolean (true or false) value.
CS1503: Argument 1: cannot convert from 'bool' to 'double'
Show potential fixes (Alt+Enter or Ctrl+.)
```

Now let's run the application and let's see if it still works.

![](img/0155736aec718cf18821e9f10a5d308d_1057_0.png)

Yes, it comes up, and you can see here the output from the SimpleStack of double and here the output from the SimpleStack of string. In the next chapter, let's wrap up the advantages of the generic SimpleStack implementation.

## Chapter 4 Advantages of Generics

To make our SimpleStack class work not only with doubles, but with any type, you have learned about different approaches Previously. First, you learned about the object approach. Using the object type instead of double meant that we were able to reuse the existing code. But with this approach, we lost two important features.

```csharp
public class SimpleStack
{
    public void Push(object item) { }
}
```

Our SimpleStack class was not type safe anymore and we were able to push any type into the stack. We also lost performance because value types, like double values, were boxed into an object container, and when you read them from the stack, you need to unbox them again with a casting. This boxing and unboxing means that in .NET memory, copy operations are necessary, and these copy operations cost performance, which is especially important when you work with a lot of data. So, after the object approach, we used copy and paste. For every type that we wanted to support, like double and string, we have copied and pasted the SimpleStack class. This means we got type safety and performance, but we were not able to reuse the code like with the object approach. So, you see, both approaches have their own advantages, but you don't get all three advantages with these two approaches. And this is where generics enters the stage.

```csharp
public class SimpleStackDouble
{
    public void Push(double item) { }
}

public class SimpleStackString
{
    public void Push(string item) { }
}
```

With generics, you get all these advantages that you see here. You can reuse your code. We have written in this chapter just a single SimpleStack class that works with any type because it is generic. It is also type safe. When you create, for example, a SimpleStack of double and you try to push a string or any other type that is not a double into that stack, your code does not compile. It is also performant.

```csharp
var stack = new SimpleStack<double>();

stack.Push("Thomas"); // Does not compile
```

When you create a SimpleStack of double, the Push method takes a double, which means the double doesn't have to be boxed into an object container.

```csharp
var stack = new SimpleStack<double>();

stack.Push(2.8); // No boxing
```

These are the advantages of generics in C#. Now let's use the generic Stack class of .NET. .NET contains many generic classes, maybe the most famous generic classes are the collection classes in the namespace System.Collections.Generic. This namespace contains several generic classes, including the List of T class, the Queue of T class, the Stack of T class, and the generic dictionary class that has the two generic type parameters, TKey and TValue. To create an instance of this generic dictionary, you use the class with two type arguments that are separated with a comma, like here, int and string.

```csharp
var dictionary = new Dictionary<int, string>();
```

So here, the dictionary.Add method takes an integer and a string as arguments. But now, in this chapter, let's focus on the generic stack of T class. The Stack of T class has, like the SimpleStack of T class that we have implemented in this chapter, the Push method, a Count property, and a Pop method. This means in the console application that we have built you can use the Stack of T class instead of our SimpleStack class without changing any other code, as it works exactly the same way. Now in this demonstration, let's do this. Let's use the Stack of T class of .NET. Here I've opened the Program.cs file of our console application. Now down here in the StackDoubles method where we create a SimpleStack of double, let's remove the Simple from the class name and let's use the Stack class.
