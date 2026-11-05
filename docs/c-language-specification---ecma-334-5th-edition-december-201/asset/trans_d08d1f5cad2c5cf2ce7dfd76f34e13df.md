
### 13.10.6 throw 语句

throw 语句抛出异常。

```
throw-statement:
    throw expression_opt ;
```

带表达式的 throw 语句会抛出通过求值表达式产生的异常。表达式应可隐式转换为 `System.Exception`，并且在抛出之前，求值表达式的结果会被转换为 `System.Exception`。如果转换结果为 `null`，则会改为抛出 `System.NullReferenceException`。

不带表达式的 throw 语句只能在 `catch` 块中使用，在这种情况下，该语句会重新抛出当前正由该 `catch` 块处理的异常。

由于 throw 语句无条件地将控制权转移到别处，因此 throw 语句的终点永远不可达。

当抛出异常时，控制权会转移到能够处理该异常的外层 `try` 语句中的第一个 `catch` 子句。异常从被抛出点到控制权转移到合适的异常处理程序为止所发生的过程称为 *异常传播*。异常的传播包括反复评估以下步骤，直到找到匹配该异常的 `catch` 子句为止。在此描述中，*抛出点* 最初是异常被抛出的位置。

- 在当前函数成员中，会检查每个包含抛出点的 `try` 语句。对于每个语句 S，从最内层的 `try` 语句开始，到最外层的 `try` 语句结束，按顺序评估以下步骤：
  - 如果 S 的 `try` 块包含抛出点并且 S 具有一个或多个 `catch` 子句，则按出现顺序检查 `catch` 子句以定位异常的合适处理程序。第一个指定异常类型 T（或在运行时表示异常类型 T 的类型参数）的 `catch` 子句，只要运行时类型 E 派生自 T，就被视为匹配。一般 `catch`（§13.11）子句被视为与任何异常类型匹配。如果找到匹配的 `catch` 子句，则通过将控制权转移到该 `catch` 子句的块来完成异常传播。
  - 否则，如果 S 的 `try` 块或 `catch` 块包含抛出点并且 S 具有 `finally` 块，则控制权会转移到 `finally` 块。如果 `finally` 块抛出另一个异常，则当前异常的处理将被终止。否则，当控制权到达 `finally` 块的终点时，当前异常的处理会继续。
- 如果在当前函数调用中未找到异常处理程序，则函数调用将被终止，并发生以下情况之一：
  - 如果当前函数是非 async，则以上步骤会针对调用该函数的调用者重复执行，抛出点对应于调用该函数成员的语句。
  - 如果当前函数是 async 且返回 task，则异常会被记录在返回的 task 中，该 task 会被置于故障或取消状态，如 §15.15.2 中所述。
  - 如果当前函数是 async 且返回 void，则当前线程的同步上下文会按 §15.15.3 中所述进行通知。
- 如果异常处理终止了当前线程中的所有函数成员调用，表明该线程没有处理该异常的处理程序，则该线程本身将被终止。此类终止的影响由实现定义。

## 13.11 try 语句

try 语句提供了一种在块执行期间捕获异常的机制。此外，try 语句还提供了指定在控制权离开 try 语句时始终执行的代码块的能力。

```
try-statement:
    try block catch-clauses
    try block catch-clauses_opt finally-clause

catch-clauses:
    specific-catch-clauses
    specific-catch-clauses_opt general-catch-clause

specific-catch-clauses:
    specific-catch-clause
    specific-catch-clauses specific-catch-clause

specific-catch-clause:
    catch ( type identifier_opt ) block

general-catch-clause:
    catch block

finally-clause:
    finally block
```

try 语句有三种可能的形式：

- 后跟一个或多个 catch 块的 try 块。
- 后跟 finally 块的 try 块。
- 后跟一个或多个 catch 块再跟 finally 块的 try 块。

当 catch 子句指定一个类型时，该类型应为 System.Exception 或派生自 System.Exception 的类型。当 catch 子句指定类型参数时，它应为有效基类为或派生自 System.Exception 的类型参数类型。

当 catch 子句同时指定类类型和标识符时，会声明给定名称和类型的异常变量。异常变量对应于作用域扩展到 catch 块上的局部变量。在 catch 块执行期间，异常变量表示当前正在处理的异常。就确定性赋值检查而言，异常变量在其整个作用域内被视为已确定赋值。

除非 catch 子句包含异常变量名，否则在 catch 块中无法访问异常对象。

不指定异常类型也不指定异常变量名的 catch 子句称为一般 catch 子句。try 语句只能有一个一般 catch 子句，如果存在，则它必须是最后一个 catch 子句。

> [注：某些编程语言可能支持无法表示为派生自 System.Exception 的对象的异常，尽管此类异常永远不会由 C# 代码生成。一般 catch 子句可能用于捕获此类异常。因此，一般 catch 子句在语义上不同于指定类型 System.Exception 的子句，因为前者还可能捕获来自其他语言的异常。结束注]

为了定位异常的处理程序，catch 子句会按词法顺序检查。如果 catch 子句指定的类型与同一 try 的 earlier catch 子句中指定的类型相同或派生自该类型，则会发生编译时错误。[注：没有此限制，就可能编写不可达的 catch 子句。结束注]

在 catch 块内，可以使用不带表达式的 throw 语句（§13.10.6）重新抛出该 catch 块捕获的异常。对异常变量的赋值不会改变被重新抛出的异常。

[示例：在以下代码

```
using System;
class Test
{
    static void F() {
        try {
            G();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw; // re-throw
        }
    }
    static void G() {
        throw new Exception("G");
    }
    static void Main() {
        try {
            F();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in Main: " + e.Message);
        }
    }
}
```

方法 F 捕获异常，将一些诊断信息写入控制台，修改异常变量，然后重新抛出异常。被重新抛出的异常是原始异常，因此产生的输出为：

```
Exception in F: G
Exception in Main: G
```

如果第一个 catch 块抛出 e 而不是重新抛出当前异常，则产生的输出将如下所示：

```
Exception in F: G
Exception in Main: F
```

结束示例]

对于 break、continue 或 goto 语句将控制权转移出 finally 块而言是编译时错误。当 break、continue 或 goto 语句出现在 finally 块中时，该语句的目标必须在同一 finally 块内，否则会发生编译时错误。

在 finally 块中出现 return 语句是编译时错误。

try 语句的执行如下：

- 控制权转移到 try 块。
- 当且仅当控制权到达 try 块的终点时：
  - 如果 try 语句具有 finally 块，则执行 finally 块。
  - 控制权转移到 try 语句的终点。
- 如果在 try 块执行期间异常传播到 try 语句：
  - 如果有的话，按出现顺序检查 catch 子句以定位异常的合适处理程序。第一个指定异常类型或异常的基类型的 catch 子句
