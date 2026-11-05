
```
class A
{
    static void f()
    {
        int i, j;
        try
        {
            goto LABEL;
            // Neither i nor j definitely assigned
            i = 1;
            // i definitely assigned
        }
        catch
        {
            // Neither i nor j definitely assigned
            i = 3;
            // i definitely assigned
        }
        finally
        {
            // Neither i nor j definitely assigned
            j = 5;
            // j definitely assigned
        }
        // i and j definitely assigned
        LABEL: ;
        // j definitely assigned
    }
}
```

## 5.3.3.16 foreach 语句

对于形式为 的 foreach 语句 stmt：

foreach ( type identifier in expr ) embedded-statement

- v 在 expr 开始时的确定性赋值状态与 v 在 stmt 开始时的状态相同。
- v 在控制流转移到 embedded-statement 或 stmt 的终点时的确定性赋值状态与 v 在 expr 结束时的状态相同。

## 5.3.3.17 using 语句

对于形式为 的 using 语句 stmt：

using ( resource-acquisition ) embedded-statement

- v 在 resource-acquisition 开始时的确定性赋值状态与 v 在 stmt 开始时的状态相同。

v 在控制流转移到 embedded-statement 时的确定性赋值状态与 v 在 resource-acquisition 结束时的状态相同。

## 5.3.3.18 lock 语句

对于形式为 的 lock 语句 stmt：

```
lock ( expr ) embedded-statement
```

- v 在 expr 开始时的确定性赋值状态与 v 在 stmt 开始时的状态相同。
- v 在控制流转移到 embedded-statement 时的确定性赋值状态与 v 在 expr 结束时的状态相同。

## 5.3.3.19 yield 语句

对于形式为 的 yield return 语句 stmt：

```
yield return expr ;
```

- v 在 expr 开始时的确定性赋值状态与 v 在 stmt 开始时的状态相同。
- v 在 stmt 结束时的确定性赋值状态与 v 在 expr 结束时的状态相同。

yield break 语句对确定性赋值状态没有影响。

## 5.3.3.20 简单表达式的一般规则

以下规则适用于这些类型的表达式：字面量 (§7.6.1)、简单名称 (§7.6.2)、成员访问表达式 (§7.6.4)、非索引基访问表达式 (§7.6.8)、typeof 表达式 (§7.6.11) 和默认值表达式 (§7.6.13)。

- 这种表达式结束时 v 的确定性赋值状态与该表达式开始时 v 的确定性赋值状态相同。

## 5.3.3.21 包含嵌入表达式的表达式的一般规则

以下规则适用于这些类型的表达式：带括号的表达式 (§7.6.3)；元素访问表达式 (§7.6.6)；带索引的基访问表达式 (§7.6.8)；增量和减量表达式 (§7.6.9, §7.7.5)；转换表达式 (§7.7.6)；一元 +、-、~、* 表达式；二元 +、-、*、/、%、<<、>>、<、<=、>、>=、==、!=、is、as、&、|、^ 表达式 (§7.8, §7.9, §7.10, §7.11)；复合赋值表达式 (§7.17.2)；checked 和 unchecked 表达式 (§7.6.12)；以及数组和委托创建表达式 (§7.6.10)。

这些表达式中的每一个都有一个或多个子表达式，这些子表达式会无条件地按固定顺序求值。例如，二元 % 运算符先求值运算符的左操作数，然后求值右操作数。索引操作先求值被索引的表达式，然后按从左到右的顺序求值每个索引表达式。对于具有按该顺序求值的子表达式 expr₁、expr₂、...、exprₙ 的表达式 expr：

- v 在 expr₁ 开始时的确定性赋值状态与 v 在 expr 开始时的确定性赋值状态相同。
- v 在 exprᵢ 开始时的确定性赋值状态（i 大于 1）与 v 在 exprᵢ₋₁ 结束时的确定性赋值状态相同。
- v 在 expr 结束时的确定性赋值状态与 v 在 exprₙ 结束时的确定性赋值状态相同。

## 5.3.3.22 调用表达式和对象创建表达式

对于形式为 的调用表达式 expr：

```
primary-expression ( arg₁ , arg₂ , ... , argₙ )
```

或形式为 的对象创建表达式：

```
new type ( arg₁ , arg₂ , ... , argₙ )
```

- 对于调用表达式，v 在 primary-expression 之前的确定性赋值状态与 v 在 expr 之前的状态相同。
- 对于调用表达式，v 在 arg₁ 之前的确定性赋值状态与 v 在 primary-expression 之后的状态相同。
- 对于对象创建表达式，v 在 arg₁ 之前的确定性赋值状态与 v 在 expr 之前的状态相同。
- 对于每个参数 argᵢ，v 在 argᵢ 之后的确定性赋值状态由正常表达式规则确定，忽略任何 ref 或 out 修饰符。
- 对于每个参数 argᵢ，其中 i 大于 1，v 在 argᵢ 之前的确定性赋值状态与 v 在 argᵢ₋₁ 之后的状态相同。
- 如果变量 v 作为 out 参数（即形式为“out v”的参数）在任一参数中传递，则 v 在 expr 之后的状态为确定赋值。否则，v 在 expr 之后的状态与 v 在 argₙ 之后的状态相同。
- 对于数组初始值设定项 (§7.6.10.4)、对象初始值设定项 (§7.6.10.2)、集合初始值设定项 (§7.6.10.3) 和匿名对象初始值设定项 (§7.6.10.6)，确定性赋值状态由这些构造所定义的展开式确定。

## 5.3.3.23 简单赋值表达式

对于形式为 v = expr-rhs 的表达式 expr：

- v 在 expr-rhs 之前的确定性赋值状态与 v 在 expr 之前的确定性赋值状态相同。
- 如果 w 与 v 是同一变量，则 v 在 expr 之后的确定性赋值状态为确定赋值。否则，v 在 expr 之后的确定性赋值状态与 v 在 expr-rhs 之后的确定性赋值状态相同。

## 5.3.3.24 && 表达式

对于形式为 expr-first && expr-second 的表达式 expr：

- v 在 expr-first 之前的确定性赋值状态与 v 在 expr 之前的确定性赋值状态相同。
- v 在 expr-second 之前的确定性赋值状态如果 v 在 expr-first 之后的状态为确定赋值或“在真表达式后确定赋值”，则为确定赋值。否则，不为确定赋值。
- v 在 expr 之后的确定性赋值状态由以下确定：
  - 如果 v 在 expr-first 之后的状态为确定赋值，则 v 在 expr 之后的状态为确定赋值。
  - 否则，如果 v 在 expr-second 之后的状态为确定赋值，且 v 在 expr-first 之后的状态为“在假表达式后确定赋值”，则 v 在 expr 之后的状态为确定赋值。
  - 否则，如果 v 在 expr-second 之后的状态为确定赋值或“在真表达式后确定赋值”，则 v 在 expr 之后的状态为“在真表达式后确定赋值”。
  - 否则，如果 v 在 expr-first 之后的状态为“在假表达式后确定赋值”，且 v 在 expr-second 之后的状态为“在假表达式后确定赋值”，则 v 在 expr 之后的状态为“在假表达式后确定赋值”。
  - 否则，v 在 expr 之后的状态不为确定赋值。

在示例中

```
class A
{
    static void f(int x, int y)
    {
        int i;
        if (x >= 0 && (i = y) >= 0)
        {
            // i definitely assigned
        }
        else
        {
            // i not definitely assigned
        }
        // i not definitely assigned
    }
}
```

变量 i 在 if 语句的一个嵌入语句中被认为已确定赋值，但在另一个中未被确定赋值。在方法 F 中的 if 语句中，变量 i 在第一个嵌入语句中为确定赋值，因为表达式 (i = y) 的执行总是在该嵌入语句执行之前。相比之下，变量 i 在第二个嵌入语句中未被确定赋值，因为 x >= 0 可能测试为假，导致变量 i 未赋值。

## 5.3.3.25 || 表达式

对于形式为 expr-first || expr-second 的表达式 expr：

- v 在 expr-first 之前的确定性赋值状态与 v 在 expr 之前的确定性赋值状态相同。
- v 在 expr-second 之前的确定性赋值状态如果 v 在 expr-first 之后的状态为确定赋值或“在假表达式后确定赋值”，则为确定赋值。否则，不为确定赋值。
- v 在 expr 之后的确定性赋值状态由以下确定：
  - 如果 v 在 expr-first 之后的状态为确定赋值，则 v 在 expr 之后的状态为确定赋值。
  - 否则，如果 v 在 expr-second 之后的状态为确定赋值，且 v 在 expr-first 之后的状态为“在真表达式后确定赋值”，则 v 在 expr 之后的状态为确定赋值。
  - 否则，如果 v 在 expr-second 之后的状态为确定赋值或“在假表达式后确定赋值”，则 v 在 expr 之后的状态为“在假表达式后确定赋值”。
  - 否则，如果 v 在 expr-first 之后的状态为“在真表达式后确定赋值”，且 v 在 expr-second 之后的状态为“在真表达式后确定赋值”，则 v 在 expr 之后的状态为“在真表达式后确定赋值”。
  - 否则，v 在 expr 之后的状态不为确定赋值。
