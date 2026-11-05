

- 在 *lock 语句*的块内
- 在将匿名函数转换为表达式树类型时（§10.7.3）
- 在不安全上下文中

*注意：* *await 表达式*不能出现在 *查询表达式*中的大多数位置，因为这些位置在语法上会被转换为使用非异步 lambda 表达式。*注意结束*

在异步函数内部，*await* 不得用作 *可用标识符*，但逐字标识符 *@await* 可以使用。因此，*await 表达式*与涉及标识符的各种表达式之间不存在句法歧义。在异步函数外部，*await* 作为普通标识符使用。

*await 表达式*的操作数称为 *任务*。它表示一个异步操作，在求值 *await 表达式*时该操作可能已经完成，也可能尚未完成。*await* 运算符的目的是暂停封闭异步函数的执行，直到所等待的任务完成，然后获取其结果。

### 11.8.8.2 可等待表达式

*await 表达式*的任务必须是 *可等待的*。如果满足以下条件之一，则表达式 *t* 是可等待的：

- *t* 的编译时类型为 *dynamic*
- *t* 具有可访问的实例方法或扩展方法 `GetAwaiter`，没有参数且没有类型参数，其返回类型为 *A*，并且 *A* 满足以下所有条件：
  - *A* 实现接口 `System.Runtime.CompilerServices.INotifyCompletion`（以下简称 `INotifyCompletion`）
  - *A* 具有可访问、可读的类型为 *bool* 的实例属性 `IsCompleted`
  - *A* 具有可访问的实例方法 `GetResult`，没有参数且没有类型参数

`GetAwaiter` 方法的用途是为任务获取 *等待器*。类型 *A* 称为该 await 表达式的 *等待器类型*。

`IsCompleted` 属性的用途是判断任务是否已经完成。如果已经完成，则无需挂起求值。

`INotifyCompletion.OnCompleted` 方法的用途是向任务注册一个“延续”（continuation）；即一个类型为 `System.Action` 的委托，它将在任务完成时被调用。

`GetResult` 方法的用途是在任务完成后获取任务的结果。该结果可能是成功完成（可能带有结果值），也可能是一个由 `GetResult` 方法抛出的异常。

### 11.8.8.3 await 表达式的分类

表达式 `await t` 的分类方式与表达式 `(t).GetAwaiter().GetResult()` 相同。因此，如果 `GetResult` 的返回类型是 `void`，则 *await 表达式*被归类为无。如果它具有非 void 返回类型 *T*，则 *await 表达式*被归类为类型 *T* 的值。

### 11.8.8.4 await 表达式的运行时求值

在运行时，表达式 `await t` 按如下方式求值：

- 通过求值表达式 `(t).GetAwaiter()` 获得 *等待器* *a*。
- 通过求值表达式 `(a).IsCompleted` 获得 *bool* *b*。
- 如果 b 为 false，则求值取决于 a 是否实现接口 System.Runtime.CompilerServices.ICriticalNotifyCompletion（以下简称 ICriticalNotifyCompletion）。此检查在绑定时进行；即，如果 a 的编译时类型为 dynamic，则在运行时进行；否则在编译时进行。设 r 表示恢复委托（§14.15）：
  - 如果 a 未实现 ICriticalNotifyCompletion，则对表达式 ((a) as INotifyCompletion).OnCompleted(r) 进行求值。
  - 如果 a 确实实现了 ICriticalNotifyCompletion，则对表达式 ((a) as ICriticalNotifyCompletion).UnsafeOnCompleted(r) 进行求值。
  - 随后求值被挂起，控制权返回给当前异步函数的调用方。
- 无论是紧接着之后（如果 b 为 true），还是在稍后调用恢复委托时（如果 b 为 false），都会对表达式 (a).GetResult() 进行求值。如果它返回值，则该值就是 await 表达式的结果；否则，结果为无。

等待器对接口方法 INotifyCompletion.OnCompleted 和 ICriticalNotifyCompletion.UnsafeOnCompleted 的实现应导致委托 r 最多被调用一次。否则，封闭异步函数的行为是未定义的。

## 11.9 算术运算符

### 11.9.1 一般

运算符 *、/、%、+ 和 - 称为算术运算符。

```
multiplicative_expression
: unary_expression
| multiplicative_expression '*' unary_expression
| multiplicative_expression '/' unary_expression
| multiplicative_expression '%' unary_expression
;

additive_expression
: multiplicative_expression
| additive_expression '+' multiplicative_expression
| additive_expression '-' multiplicative_expression
;
```

如果算术运算符的操作数具有编译时类型 dynamic，则该表达式是动态绑定的（§11.3.3）。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用那些具有编译时类型 dynamic 的操作数的运行时类型进行。

### 11.9.2 乘法运算符

对于形式为 x * y 的运算，应用二元运算符重载解析（§11.4.5）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型就是该运算符的返回类型。

预定义的乘法运算符如下所示。这些运算符都计算 x 和 y 的乘积。

- 整数乘法：

    ```
    int operator *(int x, int y);
    uint operator *(uint x, uint y);
    long operator *(long x, long y);
    ulong operator *(ulong x, ulong y);
    ```

  在 checked 上下文中，如果乘积超出结果类型的范围，则抛出 System.OverflowException。在 unchecked 上下文中，不报告溢出，并且超出结果类型范围的任何有效高位都会被丢弃。

- 浮点乘法：

    ```
    float operator *(float x, float y);
    double operator *(double x, double y);
    ```

  乘积按照 IEC 60559 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 是正有限值。z 是 x * y 的结果，四舍五入到最接近的可表示值。如果结果的幅值对于目标类型来说过大，则 z 为无穷大。由于舍入，即使 x 和 y 都不为零，z 也可能为零。

|   | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | -z | +0 | -0 | +∞ | -∞ | NaN |
| -x | -z | +z | -0 | +0 | -∞ | +∞ | NaN |
| +0 | +0 | -0 | +0 | -0 | NaN | NaN | NaN |
| -0 | -0 | +0 | -0 | +0 | NaN | NaN | NaN |
| +∞ | +∞ | -∞ | NaN | NaN | +∞ | -∞ | NaN |
| -∞ | -∞ | +∞ | NaN | NaN | -∞ | +∞ | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

  （除非另有说明，在 §11.9.2–§11.9.6 的浮点表中，使用“+”表示值为正；使用“-”表示值为负；没有符号表示该值可能为正、可能为负或没有符号（NaN）。）

- 十进制乘法：

    ```
    decimal operator *(decimal x, decimal y);
    ```

  如果结果值的幅值过大，无法以 decimal 格式表示，则抛出 System.OverflowException。由于舍入，即使两个操作数都不为零，结果也可能为零。在进行任何舍入之前，结果的小数位数是两个操作数的小数位数之和。十进制乘法等价于使用 System.Decimal 类型的乘法运算符。

上面定义的非提升预定义乘法运算符的提升形式（§11.4.8）也是预定义的。

### 11.9.3 除法运算符

对于形式为 x / y 的运算，应用二元运算符重载解析（§11.4.5）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型就是该运算符的返回类型。

预定义的除法运算符如下所示。这些运算符都计算 x 和 y 的商。

