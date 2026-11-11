

```csharp
static void Main()
{
    System.Console.WriteLine("Hi C#!");
}
```

## 语法

声明方法时使用以下语法：

static data_type_of_the_result name_of_method (list_of_parameters)

下面使用 Main() 方法（即 static void Main()）来分析该语法。Main() 使用 “void” 作为返回类型，因为它不产生任何结果。单词 “Main” 用作它的名称。而圆括号则充当程序员将提供的参数的容器。

重要提示：编写 C# 程序时必须遵循此语法。不要改变方法各部分的位置。

C# 不要求你在声明中包含参数。这意味着你可以将括号留空（例如 Main()）。

## 方法名称

在声明、调用或实现方法时，你需要指明方法名。命名方法时需要记住以下规则：

- 确保首字母大写。
- 每个单词都以大写字母开头（例如 SampleMethod、NewMethod、MainLine 等）。

```
;
```

如果你编译并执行该代码，命令提示符将打印以下消息：

*我喜欢狗。*

## 可以调用方法的位置

C# 允许你在以下位置调用方法：

- 在程序的主方法（即 Main()）内部。
- 在另一个方法内部。
- 在方法自身的方法体内部。这种技术称为“递归”。

### 递归方法调用^120

方法可以调用自身。此过程称为 *递归*^120。请看下面给出的阶乘示例：

```csharp
using System;
namespace MethodApplication {
    class NumberChecker {
        public int factorial(int x) {
            /* declaring a local variable */
            int answer;
            if (x == 1) {
                return 1;
            } else {
                answer = factorial(x - 1) * x;
                return answer;
            }
        }
        static void Main(string[] args) {
            NumberChecker n = new NumberChecker();
            //let's now call the factorial method
            Console.WriteLine("The factorial of 8 is : {0}", n.factorial(8));
            Console.WriteLine("The factorial of 9 is : {0}", n.factorial(9));
            Console.ReadLine();
        }
    }
}
```

我们创建了阶乘函数以及名为 *n* 的类实例。该代码将返回如下结果：

![](img/239ff1e8a63502805c86c4dfbd71509a_533_0.png)

这段代码能够给出 8 和 9 的阶乘。注意，一个数的阶乘是将小于等于该数的所有正整数相乘。例如，8 的阶乘是 1 * 2 * 3 * 4 * 5 * 6 * 7 * 8，结果为 40320，如上所示。

## 向方法传递参数

如果方法定义时带有参数，那么在调用它时应向它传递参数。可以使用三种方法向方法传递参数。下面我们来讨论这些方法。

### 按值传递

此方法会将实参的实际值复制到函数形参中。这是向方法传递参数的默认机制。使用此机制时，调用函数会为每个值参数在内存中创建新位置，然后将实参的值复制到这些位置中。这意味着在方法内部对参数所做的更改不会影响实参。

下面通过一个示例来演示：

```csharp
using System;
namespace MethodApplication {
    class NumberChecker {
        public void swap(int a, int b) {
            int temp;
            temp = a; /* saving the value of a */
            a = b;   /* putting b into a */
            b = temp; /* putting temp into b */
        }
        static void Main(string[] args) {
            NumberChecker n = new NumberChecker();

            /* defining a local variable */
            int x = 10;
            int y = 20;

            Console.WriteLine("Before swapping, value of x is : {0}", x);
            Console.WriteLine("Before swapping, value of y is : {0}", y);

            /* let’s swap the values by calling the function */
            n.swap(x, y);

            Console.WriteLine("After swapping, value of x is : {0}", x);
            Console.WriteLine("After swapping, value of y is : {0}", y);

            Console.ReadLine();
        }
    }
}
```

该代码产生以下输出：

![](img/239ff1e8a63502805c86c4dfbd71509a_535_0.png)

我们所做的是在函数内部更改了值。然而，上面的输出表明这种更改没有生效；因此它没有在上面的结果中体现出来。

这就是在 C# 中按值传递参数的方式。

### 按引用传递

引用参数引用变量的内存位置。按引用传递参数时，不会创建新的内存位置，这与按值传递的情况不同。引用参数实际上引用的内存位置与方法调用时提供的实参相同。

要声明引用参数，我们使用 *ref* 关键字。下面用一个示例来演示：

```csharp
using System;
namespace MethodApplication {
    class NumberChecker {
        public void swap(ref int a, ref int b) {
            int temp;

            temp = a; /* saving the value of a */
            a = b;   /* putting b into a */
            b = temp; /* putting temp into b */
        }
    }
}
```

值已经如上所示完成交换。上述更改反映在 *Main* 函数中。

### 按输出传递[22]

返回语句只能帮助我们从一个函数中返回单个值。然而，通过使用 *输出参数*，可以从一个函数中返回两个值。输出参数与引用参数相同，区别在于它们将数据从方法中传出，而不是传入方法。

以下示例演示了这一点：

```csharp
using System;
namespace MethodApplication {
  class NumberChecker {
    public void getValue(out int a) {
      int temp = 20;
      a = temp;
    }
    static void Main(string[] args) {
      NumberChecker n = new NumberChecker();

      /* defining a local variable */
      int x = 10;

      Console.WriteLine("Before calling the method, value of x : {0}", x);
      /* call the function to get value */
      n.getValue(out x);

      Console.WriteLine("After calling the method, the value of x is : {0}", x);
      Console.ReadLine();
    }
  }
}
```

它返回以下内容：

调用方法前，x 的值为：10  
调用方法后，x 的值为：20

为输出参数提供的变量应被赋值。当希望通过参数从方法中返回值，而又不想给参数赋初始值时，输出参数非常有用。以下示例将帮助你更好地理解这一点：

```csharp
using System;
namespace MethodApplication {
    class NumberChecker {
        public void getValues(out int a, out int b) {
            Console.WriteLine("Enter in your first value: ");
            a = Convert.ToInt32(Console.ReadLine());

            Console.WriteLine("Enter in your second value: ");
            b = Convert.ToInt32(Console.ReadLine());
        }
        static void Main(string[] args) {
            NumberChecker n = new NumberChecker();

            /* defining a local variable */
            int x, y;

            /* call a function to obtain the values */
            n.getValues(out x, out y);

            Console.WriteLine("After calling the method, the value of x is : {0}",
                x);

            Console.WriteLine("After calling the method, the value of y is : {0}",
                y);

            Console.ReadLine();
        }
    }
}
```

系统会提示你输入这两个值，请照做。随后你将看到调用方法前后这些变量的值。

