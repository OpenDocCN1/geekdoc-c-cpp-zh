

# 13.9 检查和未检查语句

对整型数值值进行操作可能会产生过大的结果。在检查性（checked）上下文中，运行时整数溢出将抛出 `OverflowException`，而编译时整数溢出将产生编译时错误。在未检查（unchecked）上下文中，编译时和运行时的整数溢出都会发生回绕（丢弃最高位），而不会抛出任何异常或编译时错误。

`checked` 语句为块语句创建一个检查性上下文；其形式如下：

```
checked
block-statement
```

`unchecked` 语句为块语句创建一个未检查性上下文；其形式如下：

```
unchecked
block-statement
```

在这两种情况下，只有文本位于块语句内部的算术操作会受影响。在块语句调用的方法中执行的算术操作不受影响，而文本位于块语句内部匿名委托表达式和 lambda 表达式中的算术操作则受影响。这些与检查和未检查表达式（第 12.3 节）类似。

# 13.10 using 语句

`using` 语句的目的是在使用后释放资源 `res`，例如文件句柄或数据库连接。该语句可能具有以下形式：

```
using type res = initializer;
body
```

这声明 `res` 的类型为 `type`，如果使用了关键字代替 `type`，则为 `initializer` 的推断类型（第 6.3 节）。初始化器被求值并将其结果赋值给 `res`，执行 `body`，最后无论 `body` 是正常终止、抛出异常还是通过 `return` 或 `continue` 退出，都会对 `res` 调用 `Dispose()`。类型必须隐式转换为 `IDisposable`，且 `body` 不能是声明语句或标记语句。变量 `res` 是只读的；不能对其赋值，也不能用作 `ref` 或参数。该语句等同于：

```
{
  type res = initializer;
  { body }
  finally { if (res != null) ((IDisposable)res).Dispose(); }
}
```

命名空间 `System` 的 `IDisposable` 接口描述了一个方法：

- 调用 `void Dispose()` 用于关闭或释放对象持有的资源，例如文件、流或数据库连接。多次调用时不得抛出异常。

# 13.11 lock 语句

`lock` 语句与线程相关，在第 21.2 节中描述。

# 示例 138 检查和未检查整数操作

`checked` 和 `unchecked` 语句仅影响文本上包含在语句内部的操作。因此，从语句调用的方法中发生的溢出不受显式溢出检查文本的影响。例如，`int.Parse("999999999")` 的调用无论在检查还是未检查上下文中，始终会抛出 `OverflowException`。

在检查上下文中，在编译时执行的溢出计算将导致编译时错误，而不是在运行时抛出异常。

```
checked {
    Console.WriteLine(int.MaxValue + 1); // 编译时错误
    Console.WriteLine(int.MinValue - 1); // 编译时错误
    Console.WriteLine((uint)(0-1)); // 编译时错误
    int i = int.Parse("999999999"); // 抛出 OverflowException
}

unchecked {
    Console.WriteLine(int.MaxValue + 1); // -2147483648 (回绕)
    Console.WriteLine(int.MinValue - 1); // 2147483647 (回绕)
    Console.WriteLine((uint)(0-1)); // 4294967295 (回绕)
    int i = int.Parse("999999999"); // 抛出 OverflowException
}
```

另参见示例 73。

# 示例 139 using 语句

`using` 语句从给定的文本文件创建一个 `TextReader` 并尝试从其中读取三个浮点数。`using` 语句确保无论块是正常终止还是抛出异常，`TextReader` 都会关闭。这种行为与示例 37 相同。

```csharp
static double[] Read(string filename) {
    using (TextReader reader = new StreamReader(filename)) {
        double[] res = new double[3];
        res[0] = double.Parse(reader.ReadLine());
        res[1] = double.Parse(reader.ReadLine());
        res[2] = double.Parse(reader.ReadLine());
        return res;
    }
}
```

# 13.12 yield 语句

`yield` 语句用于方便地定义枚举器和可枚举项（第 27.2 节）。`yield` 语句可以在方法、属性的 get 访问器或索引器内部使用，其类型为 `IEnumerable` 或 `IEnumerable<T>`。

`yield` 语句必须具有以下两种形式之一：
- `yield return;`
- `yield break;`

`yield` 的类型必须隐式转换为 `IEnumerable` 或 `IEnumerable<T>`。`yield` 语句在块语句内部执行时会产生值。当 `yield` 语句通过 `return` 结束块、或抛出异常时，块会终止。使用 `yield` 语句，`yield` 语句可以产生整数序列。

`yield` 语句不能出现在 `catch` 子句或具有 `ref` 参数的语句中。`yield` 语句可以出现在 `finally` 子句中。

| 状态 | MoveNext() | yield | 块结束 | 抛出异常 | Dispose() |
|---|---|---|---|---|
| 之前 | 恢复变量 | N/A | N/A | N/A | |
| 运行 | 未指定 | 返回 true | 状态执行后 | 状态执行后 | | |
| 挂起 | 返回 false | N/A | N/A | 未指定 | 状态执行后 |

编译器将块语句转换为实现 `IDisposable` 的类，因此它可以被调用。如果迭代器方法返回 `IEnumerable`，则状态变为**挂起**。

# 示例 140 整数序列的迭代器

`yield` 语句可以通过如下声明 `GetEnumerator` 来枚举整数序列（68 节 `Seq`）。它与返回 `Enumerator` 对象的方法的效果相同。为了满足这一点，我们使用了显式接口方法（15.3 节）。

```csharp
struct Seq : IEnumerator {
    private readonly int b, k, n;

    public IEnumerator<int> GetEnumerator() {
        for (int i=0; i<n; i++) {
            yield return b + k * i;
        }
    }
    IEnumerator IEnumerable.GetEnumerator() { return GetEnumerator(); };
}
```

# 示例 141 八皇后问题的枚举

n皇后问题的解是在 $n \times n$ 棋盘上放置 $n$ 个皇后，使得任何一个皇后都不能攻击其他皇后：在任何行、列或对角线上最多有一个皇后。对于 $n=8$，解是在普通的棋盘上。迭代器方法 `Queens(w, n)` 枚举了在 във $w+1$ 列中放置了 $w+1$ 个皇后的部分解。由此导出 `Queens(n-1, n)` 枚举了n皇后问题的所有解。

```csharp
public static IEnumerable<int[]> Queens(int w, int n) {
    if (w < 0)
        yield return int[n];
    else
        foreach (int[] sol in Queens(w-1, n)) {
            for (int r=0; r<n; r++) {
                for (int c=0; c<w; c++) {
                    if (sol[c] == r || sol[c]+(w-c) == r || sol[c]-(w-c) == r)
                        goto fail;
                }
                sol[w] = r;
                yield return sol;
                fail: {}
            }
        }
}
```

