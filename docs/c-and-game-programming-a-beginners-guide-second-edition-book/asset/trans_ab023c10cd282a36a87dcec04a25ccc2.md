

### 示例5.44：用户定义的异常

```csharp
using System;

namespace Chapter5 {
    public class MyException : System.ApplicationException {
        public MyException(string Comment) : base(Comment) {}
    }

    public class Errors {
        static void Main() {
            Errors Er = new Errors();
            Er.TryMethod();
        }

        public void TryMethod() {
            string Input;
            int X, Y;

            Console.WriteLine("Let's divide some numbers...");

            while(true) {
                Console.Write("Enter your numerator now: ");
                Input = Console.ReadLine();

                if (char.IsNumber(Input, 0)) {
                    X = int.Parse(Input);
                } else {
                    throw new IndexOutOfRangeException("\nCharacter " +
                        "Detected where Integer Value was Expected!");
                }

                Console.Write("Enter your denominator now: ");
                Input = Console.ReadLine();

                if (char.IsNumber(Input, 0)) {
                    Y = int.Parse(Input);
                } else {
                    throw new IndexOutOfRangeException("\nCharacter " +
                        "Detected where Integer Value was Expected!");
                }

                try {
                    Console.WriteLine(X / Y);
                } catch (DivideByZeroException) {
                    Console.WriteLine("Division by Zero attempted!\n");
                }
            }
        }
    }
}
```

```csharp
Console.Write("Please enter a new denominator now: ");
Y = char.Parse(Console.ReadLine());

try {
    Console.WriteLine(X / Y);
} catch {
    Console.WriteLine("Error!");
    break;
}
} catch {
    Console.WriteLine("Error Detected");
}
}
}
}
}
```

## 嵌套异常

除了创建简单的 try 块结构、catch 块和基于类的异常外，我们还可以嵌套这些异常以提供更高层次的保护。在二级 catch 异常中放置第二个 try-catch 块，可以让我们添加第三个 catch-all 块，如果错误仍未包含，该块将执行（参见示例5.45a和5.45b）。

### 示例5.45a：嵌套异常

```csharp
namespace Chapter5 {
    class Mathematics {
        public static void Division(ref int X, ref int Y) {
            if (X == 0 && Y == 0) {
                X = Y = 1;
                throw new Exception("ZeroByZeroException");
            } else
                Console.WriteLine(X/Y);
        }

        public static void Main() {
            string Input;
            int X, Y;

            Console.WriteLine("Let's divide some numbers...");

            while (true) {
                Console.Write("Enter your numerator now: ");
                Input = Console.ReadLine();
                X = int.Parse(Input);

                Console.Write("Enter your denominator now: ");
                Input = Console.ReadLine();
                Y = int.Parse(Input);

                try {
                    Division(ref X, ref Y);
                } catch (DivideByZeroException) {
                    Console.WriteLine("Attempting to divide by zero!");
                } catch (System.Exception e) {
                    Console.WriteLine(e.Message);
                    try {
                        Division(ref X, ref Y);
                    } catch {
                        Console.WriteLine("Error Detected");
                    }
                }
            }
        }
    }
}
```

### 示例5.45b：应用异常

```csharp
namespace Chapter5 {
    class Mathematics {
        public static void Division(ref int X, ref int Y) {
            if (X == 0 && Y == 0) {
                X = Y = 1;
                throw new Exception("ZeroByZeroException");
            } else
                Console.WriteLine(X/Y);
        }

        public static void Main() {
            string Input;
            int X, Y;

            Console.WriteLine("Let's divide some numbers...");

            while (true) {
                Console.Write("Enter your numerator now: ");
                Input = Console.ReadLine();

                try {
                    X = int.Parse(Input);
                } catch (System.FormatException) {
                    Console.WriteLine("\nInvalid Input Detected!");
                    continue;
                }

                Console.WriteLine("Enter your denominator now: ");
                Input = Console.ReadLine();

                try {
                    Y = int.Parse(Input);
                } catch (System.FormatException) {
                    Console.WriteLine("Invalid Input Detected - " +
                        "Calculation Terminated!\n");
                    continue;
                }

                try {
                    Division(ref X, ref Y);
                } catch (DivideByZeroException) {
                    Console.WriteLine("Attempting to divide by zero!");
                } catch (System.Exception e) {
                    Console.WriteLine(e.Message);
                    try {
                        Division(ref X, ref Y);
                    } catch {
                        Console.WriteLine("Unrecoverable Error Detected");
                    }
                }
            }
        }
    }
}
```

## 二元运算符 as

as 二元运算符允许将表达式转换为数据类型。该运算符被认为是一种更优雅的数据类型转换方式，因为它的表达式可以返回 null 数据，而不会引发异常。as 表达式还要求使用引用类型，并用于表示引用类型或对象，比如公式“expression is type”，这也等价于单独调用“expression is type? (type) expression: (type) null”（参见示例5.46）。

> null 引用指的是尚未赋值的对象；它基本上充当空白或非值，可以在以后替换。它也是任何未赋值的引用类型的默认值，并且可以用来标记不需要实际引用的位置。

### 示例5.46：as 二元运算符

```csharp
using System;
namespace Chapter5 {
    public class TestAS {
        public static void Main() {
            object MyString = new object();
            MyString = 123;

            string s = MyString as string;

            if (s != null)
                Console.WriteLine(MyString);
            else
                Console.WriteLine("Test Failed!");
        }
    }
}
```

## 委托

委托是用于封装特定方法的引用对象，这些方法包含签名和形式返回类型。委托虽然类似于 C++ 函数指针，但实际上是类型安全的，并且被认为符合 OOP（面向对象编程）规范。委托还允许使用六个关键修饰符：new、public、protected、internal、private 和 unsafe（unsafe 仅用于处理同时也是指针的参数时）。委托最常用于将方法作为参数传递。类型安全性基于签名匹配，作为其声明的一部分—委托需要在调用之前声明（参见示例5.47）。

### 示例5.47：一个简单的委托

```csharp
using System;

namespace Chapter5 {
    // Prototype
    public delegate void TryDelegate();

    public class Delegates {
        static void Main() {
            TryDelegate();
        }

        public static void TryDelegate() {
            Console.WriteLine("Hello World!");
        }
    }
}
```

## 事件

事件用于在委托之间传递信息；事件在被引用之前为 null，其属性必须同时包含 add 和 remove 访问器。事件用于指定委托并在运行时被引用；它们可以包含多个方法，并且适用于其他程序。定义事件时，我们必须确保包含一个委托。如果事件被重新定义，那么我们只需要引用该委托（参见示例5.48）。

### 示例5.48：事件

```csharp
using System.Collections;

namespace Chapter5 {
    public delegate void TryDelegate(int i);

    public class EventSetup {
        private Hashtable Test = new Hashtable();

        public event TryDelegate Event {
            add {
                Test["Event"] = (TryDelegate)Test["Event"] + value;
            }
            remove {
                Test["Event"] = (TryDelegate)Test["Event"] - value;
            }
        }
    }

    public class Events {
        public static void Main() {
        }
    }
}
```

## 预处理器指令

预处理器指令用于重定向和/或跳过不同的代码部分。由于许多复杂的原因，这变得必要，但这些指令的实际应用却相当简单。例如，我们可以定义一个代码区域，插入用于执行的子句，并包含错误警告和/或数据过滤器，从而测试特定方面和/或排查其他无法测试的子句。最常用的预处理器指令是 #region 和 #endregion 标记，它们是一组特殊的指令，可以隐藏已经测试过或过于繁琐的代码，使程序员能够更舒适地查看手头的应用程序。有关预处理器定义的完整列表，请参见表5.2（另请参见示例5.49）。

### 示例5.49：实现预处理器指令

```csharp
#define DebugTest
#define ReleaseTest

#if DebugTest
#undef DebugTest
#elif ReleaseTest
#warning "This is a warning!"
#else
#error "Error Detected"
#endif

using System;
namespace Chapter5 {
    class Class1 {
        static void Main() {}
    }
}
```

