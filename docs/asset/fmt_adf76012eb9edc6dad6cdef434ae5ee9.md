
向下转型并不总是安全的。如果`myA`证明不是`MyClassB`对象或未派生自`MyClassB`，则会发生运行时错误。

## 通用算法

在明确了向上转型（Upcasting）和向下转型之后，我们为什么需要它们？向下转型允许你做的正是在不真正知道类具体类型的情况下使用类的引用。向下转型的最极端例子是使用对象引用来处理任何你想操作的类，例如：

```
object MyAnything = new MyClassB();
((ClassB)MyAnything).methodB();
```

为什么这可能有用呢？

答案是，你可以编写仅使用对象引用就能处理任何类型的代码。简而言之，你可以编写通用算法。

换个例子，假设我们定义一个处理对象的排序方法：

```java
public object[] MySort(object[] array)
{
    //执行排序
    return array;
}
```

那么，如果我们声明一个自定义对象数组：

`MyClass[] testdata = new MyClass[10];`

我们可以使用以下代码对顺序排序：

```java
MyClass[] resultdata = (MyClass[])MySort((object[])testdata);
```

在调用中有一个到`object`的向上转型，在返回时有一个到`MyClass`的向下转型——这是我们第一次注意到输入参数与向上转型以及输出与向下转型之间的联系。这意味着该方法可以排序任何我们丢给它的类型——假设知道如何对该类型排序，即知道`MyClass[i]`是大于还是小于`MyClass[]`。

你可以通过给类提供一个`Compare`方法来为类提供顺序关系。此外，你可以通过内省（introspection）编写代码，使其仅适用于实现了`ICompare`接口的类，从而使排序更安全。在泛型引入之前的框架中可以找到许多实用的示例，见下一章。

这是一个使用类型转换来实现通用算法的极端例子。在许多情况下，函数将接受一个基类，并得益于向上转型与它及其所有派生类一起工作。`public base[]`

```java
{
    //执行排序
    return array;
}
```

这允许你传递基类或派生类的任何对象。`MyFunction`只能利用基类已有的方法，除非它向下转型到适当的派生类，但问题在于如何确保它正在处理正确的派生类。函数的结果以基类型数组的形式返回，通常这必须向下转型为传入函数的对象的类型。当然，向下转型过程中的任何错误都会导致运行时错误，因为这些错误在编译时无法被发现。简单来说，这种编写通用算法的方法是不安全的。

如果你通过使用类型转换放弃了强类型，这就是你必须面对的排序问题。替代方法是使用泛型，如下一章概述。

### 类型转换与重写

你需要意识到，虚（virtual）与非虚的考虑在向上转型和向下转型中都适用。如果方法被定义为虚的，则它是后期绑定（late bound）。如果方法不是虚的，或者使用了`new`饰符，则是早期绑定（early bound）。类型转换的方法在第5章中描述过。如果`ClassB`继承自`ClassA`并重写了方法，那么：

```java
ClassA myA = new ClassB();
myA.Method();
```

如果方法是虚的，则会调用`ClassB`上定义的方法；如果不是，则会调用`ClassA`上定义的方法。向下转型的考虑也是类似的，但情况稍微复杂一点，因为正如提到的，向下转型通常涉及到向上转型。向下转型总是早期绑定的，但任何向上转型取决于方法是如何声明的。假设假设我们有三个形成继承链的类，且每个方法都是非虚的，因此是早期绑定的：

```java
class ClassA {
    public void MyMethod() {
        Console.WriteLine("A");
    }
}
class ClassB : ClassA {
    public void MyMethod() {
        Console.WriteLine("B");
    }
}
class ClassC : ClassB {
    public void MyMethod() {
        Console.WriteLine("C");
    }
}
```

现在我们可以实现向下转型：

```java
ClassA myA = (ClassA) new ClassC();
((ClassB)myA).MyMethod();
```

注意`myA`实际上向下转型到`ClassB`。然而，由于使用了早期绑定，我们看到的是`ClassB`方法。当调用方法时，`myA`的声明类型是`ClassB`。如果你将`ClassA MyMethod`改为虚的并重写它，你会发现没有变化且调用的是`ClassB`方法——仍然使用的是早期绑定。最后，如果你也将`ClassC MyMethod`改为重写，则调用的是`ClassC`方法——最后的向上转型使用的是后期绑定（late bound），并且你可以打印。

### 值类型数组

之前的排序方法示例为我们带来了一个类型转换讨论较少的有趣问题。这并不是一个理论点，而是一个为了让语言更高效的实际决策。当这种情况发生时，可能会让你困惑一段时间。你可能认为之前的处理对象的示例可以这样做：

```java
int[] testdata = new int[] { 1, 2, 3 };
int[] result = MySort((object[])testdata);
```

毕竟，类型转换本身没有问题，系统应该自动将整数装箱（box）到可以转换为对象的引用类型中。然而，为了避免这种写法并导致许多整数的高效装箱，你会看到错误信息：

`Cannot convert from int[] to object[]`

这导致一些程序员得出结论：你不能转换数组。只要维度相同你就可以转换数组，但你不能将数组转换为引用类型数组，因为这是一个非常消耗资源的过程。似乎没有更好的方法通过迭代将值类型数组转换为引用类型数组——即使这一事实被`Copy`方法隐藏了。例如，你可以使用`Array`静态类和`Copy`方法，它会在拷贝期间对每个元素执行转换：

```java
int[] testdata = new int[] { 1, 2, 3 };
object[] objdata = new object[testdata.Length];
Array.Copy(testdata, objdata, testdata.Length);
object[] result = MySort(objdata);
```

注意数组大小必须匹配，由于同样的原因你不能将`object[]`转回`int[]`，即拆箱效率低下。你也可以使用`Array`静态类中新的泛型方法在不使用中间数组的情况下编写整个过程：

```java
object[] result = MySort(
Array.ConvertAll<int, object>(testdata,
delegate(int i){return(object)i});
```

但也将执行从`object[]`到`int[]`的转换。无论你如何处理这个问题，它都是杂乱的，因为从引用变量移动到值变量时，为了通过向上转型到`object`来工作的方法语法必须更改。更好的解决方案部分由自定义转换提供。

### 自定义类型转换

你可以编写在对你的类执行类型转换时调用的方法。然而，你不能定义到或或从基类的自定义转换。除了与值类型之间的转换外，很难看出你可能创建什么样的自定义转换。例如，如果你想允许`MyClassB`被自定义转换成`int`，你可能会添加类似的内容：

```java
class MyClassB{
    public int Value=42;
    public static explicit operator int(ClassB MyB)
    {
        return MyB.Value;
    }
}
```

这只是返回存储在实例变量中的值，但在实践中你可以返回更复杂的内容。所有转换运算符都必须声明为静态，但你可以根据转换的风格在显式（explicit）和隐式（implicit）之间进行选择。显式自定义转换始终必须写成转换的形式，但隐式转换可以交给编译器处理。

遵循这个定义，你可以编写如下代码：

```java
ClassB MyB = new MyClassB();
int v = (int)MyB;
```

有一种观点认为，如果你想进行这种自定义类型转换，定义一个`ToInt`方法比定义自定义转换更清晰，但你可以决定哪种适合你的方法。

## The Cast System

Now that we have looked in detail at casting, you can begin to see what it is really all about. Casting is really to do with introducing a little organized freedom into the type system so object-oriented programming is more flexible. That is, the primary purpose of a cast is to change the type of an object, not to change its representation. Without this facility there are a lot of things that would be much more difficult to do.

It is argued that casting really shouldn't be involved in active type conversion because it confuses the issue. If you want to be "pure" it might be better to implement all active type conversion as methods. To demonstrate how confusing this can be, consider the following example where an object downcast to an int (this is also an example of explicit boxing):

```
object MyAnything;
int MyIntA = 3;
MyAnything = MyIntA;
```

To convert back an int (to undo the int) all you have to use is a simple cast:

```
int MyIntB = (int) MyAnything;
```

This works, but what about:

`MyLong = (long) MyAnything;`

This looks as if it is the same sort of cast, but it doesn't work because it is attempting two sorts of type conversion in one go. You can't downcast Anything to an int and perform the active widening conversion needed to go from an int to a long in one. The reason is that the boxed int can only be unboxed to an int and not to another type. The correct way to do it is the rather ugly:

```
MyLong = (long) (int) MyAnything;
```

The first downcast/unboxing and then the explicit widening cast are needed to make it work.

## Variance and Casting

You may not have noticed, but the role of input and output parameters forces on a particular type of behavior when it comes to casting. This is usually called "variance" and is something that is generally introduced as part of generics. However variance is also part of casting.

To see the difference between input and output consider three classes, `MyClassA`, `MyClassB` and `MyClassC`, where `MyClassC` inherits from `MyClassB` which inherits from `MyClassA`.

Now consider a function that has `MyClassB` as its input parameter:

`myFunction(MyClassB parameter)`

An input parameter is something that is going to be worked on by the method assuming that it is a `MyClassB` object and so it could be substituted by a derived class, i.e. a bigger object such as a `MyClassC` object for example.

Now you can downcast the `MyClassB` parameter and call the function with anything derived from `MyClassC`, but you cannot use `MyClassA` because it might not have all the methods of a `MyClassB` object. This ability to accept a bigger object but not a smaller one, ie you can only downcast the parameter, is often referred to as "contravariance"

Consider the situation with respect to a return value of type `MyClassB`,

`MyClassB myFunction();`

In this case the calling program receives a `MyClassB` object as the result and can safely use it as a `MyClassA` object by upcasting from the result, but clearly you can't use it as a `MyClassC` object by downcasting. That is, the return parameter can be safely upcast to a smaller object and this in turn is referred to as "covariance"

That is if the input and output are of type `MyClassB` then:

- an input parameter can be downcast

- an input parameter can be upcast

or

output input

`MyClassA` | `MyClassB` | `MyClassC`

So in the current input parameters are contravariant, output parameters are covariant and in/out parameters are invariant because they can't be safely cast in either direction at all. The reason for this terminology and the idea is explained in more detail in Chapter 10.

## Postulate

When you realize how confused the use of casting is in C# and most modern languages you can't help but be unhappy about it. If you want to be "pure" it might be better to implement all active type conversion as methods.

开头的`<T>`声明了类型参数。你不一定使用`T`作为类型参数的名称，并且可以根据需要定义任意数量的类型参数。在函数定义内部，类型参数直接用`T`使用，不带尖括号。接下来我们可以调用该泛型函数：

```
MyClassA my1 = new MyClassA();
MyClassA my2 = new MyClassA();
MyClassA my3 = new MyClassA();
MyClassA[] classes = { my1, my2, my3 };
```

`Boolean result = new MyClassA<object>(classes, my2);`

`Console.WriteLine(result);`
