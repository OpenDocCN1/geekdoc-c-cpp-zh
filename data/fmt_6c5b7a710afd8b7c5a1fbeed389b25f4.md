
```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse;          // myMammal refers to a Horse
...
Horse myHorseAgain = myMammal as Horse;  // OK - myMammal was a Horse
...
Whale myWhale = new Whale(...);
myMammal = myWhale;
...
myHorseAgain = myMammal as Horse;      // returns null - myMammal was a Whale
```

## Declaring new methods

One of the hardest tasks in the realm of computer programming is thinking up unique and meaningful names for identifiers. If you are defining a method for a class and that class is part of an inheritance hierarchy, sooner or later you are going to try to reuse a name that is already in use by one of the classes further up the hierarchy. If a base class and a derived class happen to declare two methods that have the same signature, you will receive a warning when you compile the application.

### Note

The method signature refers to the name of the method and the number and types of its parameters, but not its return type. Two methods that have the same name and that take the same list of parameters have the same signature, even if they return different types.

A method in a derived class masks (or hides) a method in a base class that has the same signature. For example, if you compile the following code, the compiler generates a warning message informing you that `Horse.Talk` hides the inherited method `Mammal.Talk`:

```
class Mammal
{
    ...
    public void Talk() // assume that all mammals can talk
    {
        ...
    }
}

class Horse : Mammal
{
    ...
    public void Talk()  // horses talk in a different way from other mammals!
    {
        ...
    }
}
```

Although your code will compile and run, you should take this warning seriously. If another class derives from `Horse` and calls the `Talk` method, it might be expecting the method implemented in the `Mammal` class to be called. However, the `Talk` method in the `Horse` class hides the `Talk` method in the `Mammal` class, and the `Horse.Talk` method will be called instead. Most of the time, such a coincidence is at best a source of confusion, and you should consider renaming methods to avoid clashes. However, if you’re sure that you want the two methods to have the same signature, thus hiding the `Mammal.Talk` method, you can silence the warning by using the `new` keyword, as follows:

```
class Mammal
{
    ...
    public void Talk()
    {
        ...
    }
}

class Horse : Mammal
{
    ...
    new public void Talk()
    {
        ...
    }
}
```

Using the `new` keyword like this does not change the fact that the two methods are completely unrelated and that hiding still occurs. It just turns the warning off. In effect, the `new` keyword says, “I know what I’m doing, so stop showing me these warnings.”

## Declaring virtual methods

Sometimes, you do want to hide the way in which a method is implemented in a base class. As an example, consider the `ToString` method in `System.Object`. The purpose of `ToString` is to convert an object to its string representation. Because this method is very useful, it is a member of the `System.Object` class, thereby automatically providing all classes with a `ToString` method. However, how does the version of `ToString` implemented by `System.Object` know how to convert an instance of a derived class to a string? A derived class might contain any number of fields with interesting values that should be part of the string. The answer is that the implementation of `ToString` in `System.Object` is actually a bit simplistic. All it can do is convert an object to a string that contains the name of its type, such as “`Mammal`” or “`Horse`.” This is not very useful after all. So why provide a method that is so useless? The answer to this second question requires a bit of detailed thought.

Obviously, `ToString` is a fine idea in concept, and all classes should provide a method that can be used to convert objects to strings for display or debugging purposes. It is only the implementation that requires attention. In fact, you are not expected to call the `ToString` method defined by `System.Object`; it is simply a placeholder. Instead, you might find it more useful to provide your own version of the `ToString` method in each class you define, overriding the default implementation in `System.Object`. The version in `System.Object` is there only as a safety net, in case a class does not implement or require its own specific version of the `ToString` method.

A method that is intended to be overridden is called a `virtual` method. You should be clear on the difference between *overriding* a method and *hiding* a method. Overriding a method is a mechanism for providing different implementations of the same method—the methods are all related because they are intended to perform the same task, but in a class-specific manner. Hiding a method is a means of replacing one method with another—the methods are usually unrelated and might perform totally different tasks. Overriding a method is a useful programming concept; hiding a method is often an error.

You can mark a method as a virtual method by using the `virtual` keyword. For example, the `ToString` method in the `System.Object` class is defined like this:

```
namespace System
{
    class Object
    {
        public virtual string ToString()
        {
            ...
        }
        ...
    }
    ...
}
```

### Note

If you have experience developing in Java, you should note that C# methods are not `virtual` by default.

## Declaring `override` methods

If a base class declares that a method is `virtual`, a derived class can use the `override` keyword to declare another implementation of that method, as demonstrated here:

```
class Horse : Mammal
{
    ...
    public override string ToString()
    {
        ...
    }
}
```

The new implementation of the method in the derived class can call the original implementation of the method in the base class by using the `base` keyword, like this:

```
public override string ToString()
{
    string temp = base.ToString();
```

使用 `virtual` 和 `override` 关键字声明多态方法（在侧边栏“Virtual methods and polymorphism”中讨论）时，你必须遵循以下重要规则：

- 虚方法不能是私有的；它旨在通过继承向其他类公开。同样，`override` 方法也不能是私有的，因为一个类不能更改其继承的方法的保护级别。但是，`override` 方法可以具有一种特殊的隐私形式，即受保护访问，如你在下一节中将会发现。

- 虚方法和 `override` 方法的签名必须完全相同；它们必须具有相同的名称、参数数量和参数类型。此外，两个方法必须返回相同的类型。

- 你只能覆盖虚方法。如果基类方法不是虚的，而你尝试覆盖它，你会得到编译时错误。这是有道理的；是否允许覆盖基类的方法应由基类设计者决定。

- 如果派生类没有使用 `override` 关键字声明该方法，它不会覆盖基类方法；它会隐藏该方法。换句话说，它成为一个完全不同的方法的实现，只是恰好同名。如前所述，这将导致编译时警告，你可以通过使用 `new` 关键字来消除该警告，如前所述。

- `override` 方法是隐式虚的，可以在进一步的派生类中再次被覆盖。但是，你不允许通过使用 `virtual` 关键字显式声明 `override` 方法为虚的。

## Virtual methods and polymorphism

使用虚方法，你可以根据在运行时动态确定的对象类型调用同一方法的不同版本。考虑以下定义了对前面描述的 `Mammal` 层次结构的一种变体的类的示例：

```
class Mammal
{
    ...
    public virtual string GetTypeName()
    {
        return "This is a mammal" ;
    }
}
```

```
class Horse : Mammal
{
    ...
    public override string GetTypeName()
    {
        return "This is a horse";
    }
}

class Whale : Mammal
{
    ...

public override string GetTypeName()
    {
        return "This is a whale";
    }
}

class Aardvark : Mammal
{
    ...
}
```

有两点你应该注意：首先是 `Horse` 和 `Whale` 类中 `GetTypeName` 方法使用的 `override` 关键字，其次是 `Aardvark` 类没有 `GetTypeName` 方法这一事实。

现在检查以下代码块：

```
Mammal myMammal;
Horse myHorse = new Horse(...);
Whale myWhale = new Whale(...);
Aardvark myAardvark = new Aardvark(...);

myMammal = myHorse;
Console.WriteLine(myMammal.GetTypeName()); // Horse
myMammal = myWhale;
Console.WriteLine(myMammal.GetTypeName()); // Whale
myMammal = myAardvark;
Console.WriteLine(myMammal.GetTypeName()); // Aardvark
```
