

Code_To_Try
Possibly_Throw_An_Exception
More_Code
}

下面是一个包含 throw 语句的 try 块示例（摘自 Display 18.2）：

```
try
{
    cout << "Enter number of donuts:\n";
    cin >> donuts;
    cout << "Enter number of glasses of milk:\n";
    cin >> milk;

    if (milk <= 0)
        throw donuts;

    dpg = donuts/static_cast<double>(milk);
    cout << donuts << " donuts.\n"
         << milk << " glasses of milk.\n"
         << "You have " << dpg
         << " donuts for each glass of milk.\n";
}
```

下面的语句抛出一个 int 类型的值 donuts：

```
throw donuts;
```

被抛出的值（在此例中是 donuts）有时被称为异常；执行 throw 语句称为抛出异常。你可以抛出任何类型的值。在这个例子中，抛出的是一个 int 值。

当有东西被“抛出”时，它从一个地方移到另一个地方。在 C++ 中，从一个地方移到另一个地方的是控制流（以及被抛出的值）。当异常被抛出时，周围的 try 块中的代码停止执行，另一段称为 catch 块的代码开始执行。执行 catch 块称为捕获异常或处理异常。当异常被抛出时，它最终应该由某个 catch 块处理（捕获）。在 Display 18.2 中，相应的 catch 块紧跟在 try 块之后。下面我们重复一下这个 catch 块：

```
catch(int e)
{
    cout << e << " donuts, and No Milk!\n"
         << "Go buy some milk.\n";
}
```

## throw 语句

## 语法

```
throw Expression_for_Value_to_Be_Thrown;
```

当 throw 语句执行时，包含它的 try 块的执行被停止。如果 try 块后面跟着一个合适的 catch 块，那么控制流就会转移到 catch 块。throw 语句几乎总是嵌入在分支语句（如 if 语句）中。抛出的值可以是任何类型。

## 示例

```
if (milk <= 0)
    throw donuts;
```

这个 catch 块看起来非常像一个带有 int 类型参数的函数定义。它并不是函数定义，但在某些方面，catch 块就像函数。它是一段独立的代码，当你的程序遇到（并执行）以下语句时（在前面的 try 块内），就会执行这段代码：

```
throw Some_int;
```

因此，这个 throw 语句类似于函数调用，但它不是调用函数，而是调用 catch 块并指定执行 catch 块中的代码。catch 块通常被称为异常处理器（exception handler），这个术语表明 catch 块具有类似函数的性质。

在下面来自 catch 块的一行中，标识符 e 是什么？

```
catch(int e)
```

这个标识符 e 看起来像一个参数，而且行为也很像参数。事实上，catch 块标题中的标识符（如 e）称为 catch 块参数。每个 catch 块最多只能有一个 catch 块参数。catch 块参数有两个作用：

即被抛出的值。我们当前的示例只有一个 catch 块。catch 块参数的常用名称是 e，但你可以在 e 的位置使用任何合法的标识符。

让我们看看 Display 18.2 中的 catch 块是如何工作的。当一个值被抛出时，try 块中代码的执行结束，控制权转移到紧接在 try 块之后的 catch 块（或一组 catch 块）。Display 18.2 中的 catch 块在这里重现：

```
catch(int e)
{
    cout << e << " donuts, and No Milk!\n"
        << "Go buy some milk.\n";
}
```

当一个值被抛出时，为了使这个特定的 catch 块适用，被抛出的值必须是 int 类型。在 Display 18.2 中，被抛出的值由变量 donuts 给出，因为 donuts 是 int 类型，所以这个 catch 块能够捕获被抛出的值。

假设 donuts 的值为 12，milk 的值为 0，如 Display 18.2 中的第二个示例对话所示。由于 milk 的值不是正数，if 语句中的 throw 语句被执行。在这种情况下，变量 donuts 的值被抛出。当 Display 18.2 中的 catch 块捕获到 donuts 的值时，donuts 的值被代入 catch 块参数 e，然后执行 catch 块中的代码，产生以下输出：

```
12 donuts, and No Milk!
Go buy some milk.
```

如果 donuts 的值为正，则 throw 语句不会被执行。在这种情况下，整个 try 块都会被执行。当 try 块中的最后一条语句执行完后，会执行 catch 块之后的语句。注意，如果没有异常被抛出，catch 块会被忽略。

这一讨论听起来像是 try–throw–catch 结构与 if–else 语句等价。除了被抛出的值以外，它几乎是等价的。try–throw–catch 结构就像 if–else 语句，但额外具备向其中一个分支发送消息的能力。这听起来与 if–else 语句没有太大区别，但在实践中却有很大不同。

以更正式的语气总结：try 块包含一些代码，我们假设其中包含 throw 语句。throw 语句通常只在异常情况下执行，但一旦执行，它会抛出某种类型的值。当异常（如 Display 18.2 中的值 donuts）被抛出时，try 块结束。try 块中其余所有代码都被忽略，控制权传递给合适的 catch 块。catch 块只适用于紧邻其前面的 try 块。如果异常被抛出，那么该异常对象会被代入 catch 块参数，并执行 catch 块中的语句。例如，如果你查看 Display 18.2 中的对话，你会发现一旦用户输入一个非正数，try 块就会停止，catch 块开始执行。目前，我们将

## catch 块参数

catch 块参数是 catch 块标题中的一个标识符，它充当可能被抛出的异常（值）的占位符。当前面的 try 块中抛出一个合适的值时，该值会被代入 catch 块参数。（为了使 catch 块执行，被抛出的值必须与其 catch 块参数指定的类型一致。）你可以使用任何合法（非保留字）标识符作为 catch 块参数。

## 示例

```
catch(int e)
{
    cout << e << " donuts, and No Milk!\n"
         << "Go buy some milk.\n";
}
```

e 就是 catch 块参数。

假设每个 try 块后面都跟着一个合适的 catch 块。稍后我们将讨论没有合适的 catch 块时会发生什么。

如果在 try 块中没有抛出异常（值），那么当 try 块执行完毕后，程序继续执行 catch 块之后的代码。换句话说，如果没有异常抛出，catch 块会被忽略。在程序执行的大多数时候，throw 语句不会被执行，因此在大多数情况下，try 块中的代码会一直运行到结束，而 catch 块中的代码会被完全忽略。

## try-throw-catch

抛出和捕获异常的基本机制是 try-throw-catch 序列。throw 语句抛出异常（一个值）。catch 块捕获异常（该值）。当异常被抛出时，try 块结束，然后执行 catch 块中的代码。catch 块执行完毕后，会执行 catch 块（或一组 catch 块）之后的代码（前提是 catch 块没有结束程序或执行其他特殊操作）。

（被抛出的异常类型必须与 catch 块参数列出的类型匹配，否则该异常不会被此 catch 块捕获。这一点将在“Multiple Throws and Catches”小节中进一步讨论。）

如果在 try 块中没有抛出异常，那么当 try 块执行完毕后，程序继续执行 catch 块或一组 catch 块之后的代码。（换句话说，如果没有异常抛出，catch 块或一组 catch 块会被忽略。）

