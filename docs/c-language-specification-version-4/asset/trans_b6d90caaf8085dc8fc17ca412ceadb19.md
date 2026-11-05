
因为 `goto` 语句无条件地将控制转移到别处，所以 `goto` 语句的终点永远无法到达。

### 8.9.4 return 语句

`return` 语句将控制返回给包含该 `return` 语句的函数成员的调用者。

```
return-statement:
    return expression_opt ;
```

没有表达式的 `return` 语句只能用在不计算值的函数成员中，即返回类型为 `void` 的方法、属性或索引器的 `set` 访问器、事件的 `add` 和 `remove` 访问器、实例构造函数、静态构造函数或析构函数。

带有表达式的 `return` 语句只能用在计算值的函数成员中，即返回类型为非 `void` 的方法、属性或索引器的 `get` 访问器，或用户定义的运算符。必须存在从表达式类型到包含该函数成员的返回类型的隐式转换 (§6.1)。

在 `finally` 块 (§8.10) 中出现 `return` 语句是编译时错误。

`return` 语句的执行如下：

- 如果 `return` 语句指定了表达式，则会计算该表达式，并通过隐式转换将其结果值转换为包含该函数成员的返回类型。转换的结果成为返回给调用者的值。
- 如果 `return` 语句被一个或多个带有关联 `finally` 块的 `try` 块所包围，则控制最初转移到最内层 `try` 语句的 `finally` 块。当且仅当控制到达 `finally` 块的终点时，控制会转移到下一个外层 `try` 语句的 `finally` 块。此过程重复进行，直到所有外层 `try` 语句的 `finally` 块都已执行完毕。
- 控制返回给包含该函数成员的调用者。

因为 `return` 语句无条件地将控制转移到别处，所以 `return` 语句的终点永远无法到达。

### 8.9.5 throw 语句

`throw` 语句抛出异常。

```
throw-statement:
    throw expression_opt ;
```

带有表达式的 `throw` 语句抛出计算表达式得到的值。表达式必须表示类类型 `System.Exception` 的值、派生自 `System.Exception` 的类类型的值，或其有效基类为 `System.Exception`（或其子类）的类型参数类型的值。如果表达式的计算结果为 `null`，则改为抛出 `System.NullReferenceException`。

没有表达式的 `throw` 语句只能在 `catch` 块中使用，在这种情况下该语句会重新抛出当前由该 `catch` 块处理的异常。

因为 `throw` 语句无条件地将控制转移到别处，所以 `throw` 语句的终点永远无法到达。

当抛出异常时，控制会转移到能够处理该异常的外层 `try` 语句中的第一个 `catch` 子句。从抛出异常的点到将控制转移到合适的异常处理程序的点所发生的过程称为 *异常传播*。异常的传播包括重复评估以下步骤，直到找到匹配该异常的 *catch* 子句。在此描述中，*throw point* 最初是抛出异常的位置。

- 在当前函数成员中，检查每个包围 throw point 的 *try* 语句。对于每个语句 S，从最内层的 *try* 语句开始，到最外层的 *try* 语句结束，评估以下步骤：
  - 如果 S 的 *try* 块包围了 throw point 且 S 具有一个或多个 *catch* 子句，则按出现顺序检查 *catch* 子句以定位适合处理异常的处理程序。第一个指定异常类型或异常类型的基类型的 *catch* 子句被视为匹配。一般 *catch* 子句 (§8.10) 被视为与任何异常类型匹配。如果找到匹配的 *catch* 子句，则通过将控制转移到该 *catch* 子句的块来完成异常传播。
  - 否则，如果 S 的 *try* 块或 *catch* 块包围了 throw point 且 S 具有 *finally* 块，则控制转移到 *finally* 块。如果 *finally* 块抛出另一个异常，则当前异常的处理终止。否则，当控制到达 *finally* 块的终点时，当前异常的处理继续。
- 如果在当前函数成员调用中未找到异常处理程序，则函数成员调用终止。然后对函数成员的调用者重复上述步骤，throw point 对应于调用该函数成员的语句。
- 如果异常处理终止了当前线程中的所有函数成员调用，表示该线程没有处理该异常的处理程序，则线程本身被终止。此类终止的影响是实现定义的。

## 8.10 try 语句

*try* 语句提供了一种在块执行期间捕获异常的机制。此外，*try* 语句提供了指定在控制离开 *try* 语句时始终执行的代码块的能力。

```
try-statement:
    try block catch-clauses
    try block finally-clause
    try block catch-clauses finally-clause

catch-clauses:
    specific-catch-clauses general-catch-clauseopt
    specific-catch-clausesopt general-catch-clause

specific-catch-clauses:
    specific-catch-clause
    specific-catch-clauses specific-catch-clause

specific-catch-clause:
    catch ( class-type identifieropt ) block

general-catch-clause:
    catch block

finally-clause:
    finally block
```

*try* 语句有三种可能的形式：

C# 语言规范

- 后跟一个或多个 catch 块的 try 块。
- 后跟 finally 块的 try 块。
- 后跟一个或多个 catch 块再跟 finally 块的 try 块。

当 catch 子句指定 class-type 时，该类型必须是 System.Exception、派生自 System.Exception 的类型，或其有效基类为 System.Exception（或其子类）的类型参数类型。

当 catch 子句同时指定 class-type 和标识符时，会声明一个具有给定名称和类型的异常变量。异常变量对应于作用域扩展到 catch 块上的局部变量。在 catch 块执行期间，异常变量表示当前正在处理的异常。对于确定性赋值检查而言，异常变量在其整个作用域内被视为已明确赋值。

除非 catch 子句包含异常变量名，否则在 catch 块中无法访问异常对象。

不指定异常类型也不指定异常变量名的 catch 子句称为一般 catch 子句。try 语句只能有一个一般 catch 子句，如果存在，则必须是最后一个 catch 子句。

某些编程语言可能支持不能表示为派生自 System.Exception 的对象的异常，尽管此类异常永远不会由 C# 代码生成。一般 catch 子句可用于捕获此类异常。因此，一般 catch 子句在语义上不同于指定类型 System.Exception 的子句，因为前者还可能捕获来自其他语言的异常。

为了定位异常的处理程序，catch 子句按词法顺序检查。如果 catch 子句指定的类型与同一 try 的 earlier catch 子句中指定的类型相同或派生自该类型，则会发生编译时错误。如果没有此限制，就有可能编写不可达的 catch 子句。

在 catch 块内，可以使用没有表达式的 throw 语句 (§8.9.5) 重新抛出由该 catch 块捕获的异常。对异常变量的赋值不会改变被重新抛出的异常。

示例中

```
using System;
class Test
{
    static void F() {
        try { G(); }
        catch (Exception e) {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw; // re-throw
        }
    }
    static void G() {
        throw new Exception("G");
    }
}
```
