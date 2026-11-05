
## 10.4.4.10 For 语句

For 语句的确定性赋值检查形式为：

```
for ( for-initializer ; for-condition ; for-iterator ) embedded-statement
```

按如下语句编写的方式进行：

```
{
    for-initializer ;
    while ( for-condition ) {
        embedded-statement ;
    LLoop:        for-iterator ;
    }
}
```

continue 语句以 for 语句为目标时，被翻译为以标签 LLoop 为目标的 goto 语句。如果 for 语句中省略了 for-condition，则确定性赋值的求值按在上述展开中将 for-condition 替换为 true 的方式进行。

## 10.4.4.11 Break、continue 和 goto 语句

由 break、continue 或 goto 语句引起的控制流转移上变量 v 的确定性赋值状态，与该语句开始时变量 v 的确定性赋值状态相同。

## 10.4.4.12 Throw 语句

对于形式为

```
throw expr ;
```

的语句 stmt，expr 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。

## 10.4.4.13 Return 语句

对于形式为

```
return expr ;
```

的语句 stmt：

- expr 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- 如果 v 是输出参数，则它必须在以下任一位置被确定性赋值：
    - expr 之后
    - 或在包含 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束时。

对于形式为：

```
return ;
```

的语句 stmt：

- 如果 v 是输出参数，则它必须在以下任一位置被确定性赋值：
    - stmt 之前
    - 或在包含 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束时。

## 10.4.4.14 Try-catch 语句

对于形式为：

```
try try-block
catch ( ... ) catch-block-1
...
catch ( ... ) catch-block-n
```

的语句 stmt：

- try-block 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- catch-block-i（任意 i）开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- stmt 的结束点上变量 v 被确定性赋值当且仅当变量 v 在 try-block 的结束点以及每个 catch-block-i（从 1 到 n 的每个 i）都被确定性赋值。

## 10.4.4.15 Try-finally 语句

对于形式为：

```
try try-block finally finally-block
```

的 try 语句 stmt：

- try-block 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- finally-block 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- stmt 的结束点上变量 v 被确定性赋值当且仅当以下至少一个为真：
    - try-block 结束点上变量 v 被确定性赋值
    - finally-block 结束点上变量 v 被确定性赋值

如果进行控制流转移（例如 goto 语句），该转移开始于 try-block 内并结束于 try-block 外，则如果 finally-block 结束点上变量 v 被确定性赋值，则在此控制流转移上变量 v 也被视为确定性赋值。（这不是仅有的条件——如果由于其他原因在此控制流转移上变量 v 被确定性赋值，则它仍被视为确定性赋值。）

## 10.4.4.16 Try-catch-finally 语句

对于形式为：

```
try try-block
catch ( ... ) catch-block-1
...
catch ( ... ) catch-block-n
finally finally-block
```

的 try-catch-finally 语句的确定性赋值分析，按如下语句进行，即一个包围 try-catch 语句的 try-finally 语句：

```
try {
    try try-block
    catch ( ... ) catch-block-1
    ...
    catch ( ... ) catch-block-n
}
finally finally-block
```

[示例：以下示例演示了 try 语句（§13.11）的不同块如何影响确定性赋值。

```
class A
{
    static void F() {
        int i, j;
        try {
            goto LABEL;
            // neither i nor j definitely assigned
            i = 1;
            // i definitely assigned
        }
        catch {
            // neither i nor j definitely assigned
            i = 3;
            // i definitely assigned
        }
        finally {
            // neither i nor j definitely assigned
            j = 5;
            // j definitely assigned
        }
        // i and j definitely assigned
LABEL:
        // j definitely assigned
    }
}
end example]

## 10.4.4.17 Foreach 语句

对于形式为：

```
foreach ( *type identifier* in *expr* ) *embedded-statement*
```

的 foreach 语句 *语句*：

- *表达式* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- 对 *嵌入语句* 或 *语句* 结束点的控制流转移上 *v* 的确定性赋值状态与 *表达式* 结束时 *v* 的状态相同。

## 10.4.4.18 Using 语句

对于形式为：

```
using ( *resource-acquisition* ) *embedded-statement*
```

的 using 语句 *语句*：

- *资源获取* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- 对 *嵌入语句* 的控制流转移上 *v* 的确定性赋值状态与 *资源获取* 结束时 *v* 的状态相同。

## 10.4.4.19 Lock 语句

对于形式为：

```
lock ( *expr* ) *embedded-statement*
```

的 lock 语句 *语句*：

- *表达式* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- 对 *嵌入语句* 的控制流转移上 *v* 的确定性赋值状态与 *表达式* 结束时 *v* 的状态相同。

## 10.4.4.20 Yield 语句

对于形式为：

```
yield return *expr* ;
```

的 yield return 语句 *语句*：

- *表达式* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- *语句* 结束时 *v* 的确定性赋值状态与 *表达式* 结束时 *v* 的状态相同。

yield break 语句对确定性赋值状态没有影响。

- expr_i（i 大于 1）开始时变量 v 的确定性赋值状态与 expr_{i-1} 结束时的确定性赋值状态相同。
- expr 结束时变量 v 的确定性赋值状态与 expr_n 结束时的确定性赋值状态相同。

## 10.4.4.24 调用表达式和对象创建表达式

如果要调用的方法是没有任何实现部分方法声明的部分方法，或是调用被省略的条件方法（§22.5.3.2），则调用后变量 v 的确定性赋值状态与调用前变量 v 的确定性赋值状态相同。否则适用以下规则：

对于形式为：

```
primary-expression ( arg₁, arg₂, ... , argₙ )
```

或对象创建表达式 expr 形式为：

```
new type ( arg₁, arg₂, ... , argₙ )
```

- 对于调用表达式，primary-expression 之前变量 v 的确定性赋值状态与 expr 之前变量 v 的状态相同。
- 对于调用表达式，argᵢ 之前变量 v 的确定性赋值状态与 primary-expression 之后变量 v 的状态相同。
- 对于对象创建表达式，argᵢ 之前变量 v 的确定性赋值状态与 expr 之前变量 v 的状态相同。
- 对于每个参数 argᵢ，argᵢ 之后变量 v 的确定性赋值状态由正常表达式规则确定，忽略任何 ref 或 out 修饰符。
- 对于每个参数 argᵢ，对于大于 1 的任意 i，argᵢ 之前变量 v 的确定性赋值状态与 argᵢ₋₁ 之后变量 v 的状态相同。
- 如果变量 v 作为 out 参数（即形式为 "out v" 的参数）在任一参数中传递，则 expr 之后变量 v 的状态被确定性赋值。否则，expr 之后变量 v 的状态与 argₙ 之后变量 v 的状态相同。
- 对于数组初始值设定项（§12.7.11.5）、对象初始值设定项（12.7.11.3）、集合初始值设定项（§12.7.11.4）和匿名对象初始值设定项（§12.7.11.7），确定性赋值状态由这些构造所定义展开的方式确定。

## 10.4.4.25 简单赋值表达式

对于形式为 w = expr-rhs 的表达式 expr：

- w 之前变量 v 的确定性赋值状态与 expr 之前变量 v 的确定性赋值状态相同。
- expr-rhs 之前变量 v 的确定性赋值状态与 w 之后变量 v 的确定性赋值状态相同。
- 如果 w 与 v 相同变量，则 expr 之后变量 v 的确定性赋值状态被确定性赋值。否则，expr 之后变量 v 的确定性赋值状态与 expr-rhs 之后变量 v 的确定性赋值状态相同。

[示例：在以下代码中

```
class A
{
    static void F(int[] arr) {
        int x;
        arr[x = 1] = x;  // ok
    }
}
```
