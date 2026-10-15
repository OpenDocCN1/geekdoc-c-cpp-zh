
一个对象引用的列表，因此向列表中添加整数或浮点数会将值装箱，以便获得一个引用。

## 清单8.5：微妙的装箱和拆箱指令

```
class DisplayFibonacci
{
    static void Main()
    {
        int totalCount;
        System.Collections.ArrayList list =
            new System.Collections.ArrayList();

        Console.Write("Enter a number between 2 and 1000:");
        totalCount = int.Parse(Console.ReadLine());

        // Execution-time error:
        // list.Add(0);  // Cast to double or 'D' suffix required.
        //                       Whether cast or using 'D' suffix,
        //                       CIL is identical.
        list.Add((double)0);
        list.Add((double)1);
        for (int count = 2; count < totalCount; count++)
        {
            list.Add(
                ((double)list[count - 1] +
                 (double)list[count - 2]));
        }

        foreach (double count in list)
        {
            Console.Write("{0}, ", count);
        }
    }
}
```

## 输出8.1

```
Enter a number between 2 and 1000:42
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597,
2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418,
317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465,
14930352, 24157817, 39088169, 63245986, 102334155, 165580141,
```

清单8.5中的代码在编译时，会在生成的CIL中产生五个装箱指令和三个拆箱指令。

- 1. 前两个装箱指令出现在对`list.Add()`的初始调用中。`ArrayList`方法的签名是`int Add(object value)`。因此，传递给该方法的任何值类型都会被装箱。
- 2. 接下来是`for`循环内对`Add()`的调用中的两个拆箱指令。`ArrayList`的索引运算符的返回值始终是`object`，因为`ArrayList`包含的就是`object`。要将这两个值相加，你需要将它们强制转换回`double`。这种从对象引用到值类型的强制转换是以拆箱调用的方式实现的。
- 3. 现在，你将加法结果放入`ArrayList`实例中，这再次导致一次装箱操作。注意，前两个拆箱指令和这个装箱指令都发生在循环内。
- 4. 在`foreach`循环中，你遍历`ArrayList`中的每个项，并将这些项赋值给`count`。如前所述，`ArrayList`中的项是对象的引用，因此将它们赋给`double`实际上就是对它们逐一进行拆箱。
- 5. 在`foreach`循环中调用的`Console.WriteLine()`的签名是`void Console.Write(string format, object arg)`。因此，每次调用它都会将`double`装箱为`object`。

每次装箱操作都涉及一次分配和一次复制；每次拆箱操作都涉及一次类型检查和一次复制。使用未装箱的类型来完成相同的工作将消除分配和类型检查。显然，你可以通过消除许多装箱操作来轻松提高这段代码的性能。在最后一个`foreach`循环中使用`object`而不是`double`就是这样的改进。另一个改进是将`ArrayList`数据类型改为泛型集合（见第11章）。这里要说明的是，装箱可能是相当隐蔽的，因此开发人员需要特别注意，并留意可能反复发生并影响性能的情况。

另一个不幸的与装箱相关的问题也在运行时出现：如果你想修改最初的两个`Add()`调用，使它们不使用强制转换（或`double`字面量），你就必须把整数插入到数组列表中。由于`int`会隐式转换为`double`，这看起来是一个无害的修改。然而，`for`循环内的`double`强制转换，以及`foreach`循环中对`count`的赋值，将

```
struct Angle : IAngle
{
    // ...
    // NOTE: This makes Angle mutable, against the general
    //         guideline
    public void MoveTo(int degrees, int minutes, int seconds)
    {
        _Degrees = degrees;
        _Minutes = minutes;
        _Seconds = seconds;
    }
}
```

```
class Program
{
    static void Main()
    {
        // ...
        Angle angle = new Angle(25, 58, 23);
        object objectAngle = angle; // Box
        Console.Write(((Angle)objectAngle).Degrees);
        
        // Unbox, modify unboxed value, and discard value
        ((Angle)objectAngle).MoveTo(26, 58, 23);
        Console.Write(", " + ((Angle)objectAngle).Degrees);
        
        // Box, modify boxed value, and discard reference to box
        ((IAngle)angle).MoveTo(26, 58, 23);
        Console.Write(", " + ((Angle)angle).Degrees);
        
        // Modify boxed value directly
        ((IAngle)objectAngle).MoveTo(26, 58, 23);
        Console.WriteLine(", " + ((Angle)objectAngle).Degrees);
        
        // ...
    }
}
```

## 输出8.2

```
25, 25, 25, 26
```

清单8.7使用了`Angle`结构和`IAngle`接口。还要注意，`IAngle.MoveTo()`接口使`Angle`变得可变。这一变化暴露了可变值类型的一些特性，并以此证明了使结构体不可变的准则的重要性。

在清单8.6的前两行中，你初始化`angle`，然后将其装箱到一个名为`objectAngle`的变量中。接下来，你调用`MoveTo`将`Hours`更改为26。然而，如输出所示，第一次实际上没有发生任何更改。问题是，为了调用`MoveTo()`，编译器拆箱了`objectAngle`，并且（根据定义）制作了该值的一个副本。值类型是按值复制的——这就是它们被称为值类型的原因。尽管结果值在执行时被成功修改，但这个值的副本被丢弃，`objectAngle`引用的堆位置没有发生任何变化。

回想我们之前的类比，值类型的变量就像写着值的纸张。当你装箱一个值时，你复印了这张纸，并把复印件放进一个盒子里。当你拆箱这个值时，你复印了盒子里的纸。对第二份复印件进行编辑并不会改变盒子里的复印件。

在下一个例子中，带有注释“装箱，修改已装箱的值，并丢弃对箱的引用”的情况，出现了类似但相反的问题。不是直接调用`MoveTo()`，而是将值强制转换为`IAngle`。转换为接口类型会将值装箱，因此运行时将`angle`中的数据复制到堆上，并提供对该箱的引用。接下来，方法调用修改了所引用箱中的值。存储在变量`angle`中的值保持不变。

在最后一种情况下，强制转换为`IAngle`是引用转换，而不是装箱转换。在这种情况下，该值已经被转换为`object`而装箱，所以在此转换中不会复制该值。对`MoveTo()`的调用更新了存储在箱中的`_Hours`值，代码按预期运行。

从这个例子可以看出，可变值类型相当令人困惑，因为通常不清楚你是在修改值的副本，还是在修改你真正想要更改的存储位置。通过从一开始就避免可变值类型，你可以消除这种困惑。

> **准则**
> 
> **避免**使用可变值类型。

## 高级主题

### 如何在方法调用期间避免装箱

任何情况下，当以值类型的接收者调用方法时，接收者（在方法体内由`this`表示）必须是一个变量，而不是一个值，因为该方法可能试图修改接收者。显然，它必须是修改接收者的存储位置，而不是修改接收者值的副本然后丢弃它。清单8.7中的第二个和第四个案例说明了这一事实如何影响对已装箱值类型的方法调用的性能。

在第二种情况下，拆箱转换在逻辑上产生已装箱的值，而不是对堆上包含该箱装副本的存储位置的引用。那么，哪个存储位置作为`this`传递给修改方法调用呢？它不可能是堆上箱中的存储位置，因为拆箱转换生成的是该值的副本，而不是对该存储位置的引用。

当这种情况出现时——需要一个值类型的变量，但只有一个值可用——会发生以下两种情况之一：要么C#编译器生成代码，创建一个新的临时存储位置，并将值从箱中复制到新位置，从而使临时存储位置成为所需的变量；要么编译器产生错误并禁止该操作。在这种情况下，采用了前一种策略。新的临时存储位置随后成为调用的接收者；在它被修改后，临时存储位置被丢弃。

这个过程——对已装箱的值进行类型检查，拆箱以产生已装箱值的存储位置，分配一个临时变量，将值从箱复制到临时变量，然后使用临时存储的位置调用方法——每次使用“拆箱然后调用”模式时都会发生，无论该方法是否实际修改变量。显然，如果它不修改变量，则可以避免其中一些工作。由于C#编译器不知道你调用的某个特定方法是否会尝试修改接收者，它必须谨慎行事。

当对已装箱的值类型调用接口方法时，这些开销全部被消除。在这种情况下，如果接口方法修改了存储位置，那么接收者将是箱中的存储位置
