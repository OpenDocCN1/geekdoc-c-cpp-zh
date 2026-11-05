

或者形式如下的对象创建表达式 expr：

```
new type ( arg1, arg2, ..., argx )
```

- 对于调用表达式，v 在 primary_expression 之前的确定赋值状态与 v 在 expr 之前的状态相同。
- 对于调用表达式，v 在 arg_i 之前的确定赋值状态与 v 在 primary_expression 之后的状态相同。
- 对于对象创建表达式，v 在 arg_i 之前的确定赋值状态与 v 在 expr 之前的状态相同。
- 对于每个参数 arg_i，v 在 arg_i 之后的确定赋值状态由常规表达式规则确定，忽略任何 ref 或 out 修饰符。
- 对于每个参数 arg_i，对于任何大于 1 的 i，v 在 arg_i 之前的确定赋值状态与 v 在 arg_{i-1} 之后的状态相同。
- 如果变量 v 作为 out 实参（即形式为“out v”的实参）在任何参数中传递，则 v 在 expr 之后的状态为确定已赋值。否则，v 在 expr 之后的状态与 v 在 arg_x 之后的状态相同。
- 对于数组初始值设定项（§11.7.15.5）、对象初始值设定项（§11.7.15.3）、集合初始值设定项（§11.7.15.4）和匿名对象初始值设定项（§11.7.15.7），确定赋值状态由定义这些构造时所依据的展开确定。

### 9.4.4.25 简单赋值表达式

对于形式如下的表达式 expr：

```
w = expr_rhs
```

- v 在 w 之前的确定赋值状态与 v 在 expr 之前的确定赋值状态相同。
- v 在 expr_rhs 之前的确定赋值状态与 v 在 w 之后的确定赋值状态相同。
- 如果 w 是与 v 相同的变量，则 v 在 expr 之后的状态为确定已赋值。否则，如果赋值发生在结构类型的实例构造函数内，并且 w 是指定正在构造的实例上的自动实现属性 P 的属性访问，而 v 是 P 的隐藏后备字段，则 v 在 expr 之后的状态为确定已赋值。否则，v 在 expr 之后的状态与 v 在 expr_rhs 之后的状态相同。

示例：在以下代码中

```
class A
{
    static void F(int[] arr)
    {
        int x;
        arr[x = 1] = x; // ok
    }
}
```

*示例结束*

### 9.4.4.26 && 表达式

对于形式如下的表达式 expr：

*expr_first && expr_second*

- v 在 expr_first 之前的确定赋值状态与 v 在 expr 之前的确定赋值状态相同。
- v 在 expr_second 之前的确定赋值状态为确定已赋值，当且仅当 v 在 expr_first 之后的状态为确定已赋值或“真表达式后确定已赋值”。否则，它不是确定已赋值。
- v 在 expr 之后的状态由以下各项确定：
  - 如果 v 在 expr_first 之后的状态为确定已赋值，则 v 在 expr 之后的状态为确定已赋值。
  - 否则，如果 v 在 expr_second 之后的状态为确定已赋值，并且 v 在 expr_first 之后的状态为“假表达式后确定已赋值”，则 v 在 expr 之后的状态为确定已赋值。
  - 否则，如果 v 在 expr_second 之后的状态为确定已赋值或“真表达式后确定已赋值”，则 v 在 expr 之后的状态为“真表达式后确定已赋值”。
  - 否则，如果 v 在 expr_first 之后的状态为“假表达式后确定已赋值”，并且 v 在 expr_second 之后的状态为“假表达式后确定已赋值”，则 v 在 expr 之后的状态为“假表达式后确定已赋值”。
  - 否则，v 在 expr 之后的状态不是确定已赋值。

示例：在以下代码中

```
class A
{
    static void F(int x, int y)
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

变量 i 在 if 语句的其中一个嵌入语句中被视为确定已赋值，但在另一个中则不是。在方法 F 的 if 语句中，变量 i 在第一个嵌入语句中为确定已赋值，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相反，变量 i 在第二个嵌入语句中不是确定已赋值，因为 x >= 0 可能测试为假，导致变量 i 未被赋值。

*示例结束*

### 9.4.4.27 || 表达式

对于形式如下的表达式 *expr*：

*expr_first* || *expr_second*

- *v* 在 *expr_first* 之前的确定赋值状态与 *v* 在 *expr* 之前的确定赋值状态相同。
- *v* 在 *expr_second* 之前的确定赋值状态为确定已赋值，当且仅当 *v* 在 *expr_first* 之后的状态为确定已赋值或“假表达式后确定已赋值”。否则，它不是确定已赋值。
- *v* 在 *expr* 之后的状态由以下各项确定：
  - 如果 *v* 在 *expr_first* 之后的状态为确定已赋值，则 *v* 在 *expr* 之后的状态为确定已赋值。
  - 否则，如果 *v* 在 *expr_second* 之后的状态为确定已赋值，并且 *v* 在 *expr_first* 之后的状态为“真表达式后确定已赋值”，则 *v* 在 *expr* 之后的状态为确定已赋值。
  - 否则，如果 *v* 在 *expr_second* 之后的状态为确定已赋值或“假表达式后确定已赋值”，则 *v* 在 *expr* 之后的状态为“假表达式后确定已赋值”。
  - 否则，如果 *v* 在 *expr_first* 之后的状态为“真表达式后确定已赋值”，并且 *v* 在 *expr_second* 之后的状态为“真表达式后确定已赋值”，则 *v* 在 *expr* 之后的状态为“真表达式后确定已赋值”。
  - 否则，*v* 在 *expr* 之后的状态不是确定已赋值。

*示例：* 在以下代码中

```
class A
{
    static void G(int x, int y)
    {
        int i;
        if (x >= 0 || (i = y) >= 0)
        {
            // i not definitely assigned
        }
        else
        {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```

变量 `i` 在 `if` 语句的其中一个嵌入语句中被视为确定已赋值，但在另一个中则不是。在方法 `G` 的 `if` 语句中，变量 `i` 在第二个嵌入语句中为确定已赋值，因为表达式 `(i = y)` 的执行总是先于该嵌入语句的执行。相反，变量 `i` 在第一个嵌入语句中不是确定已赋值，因为 `x >= 0` 可能测试为真，导致变量 `i` 未被赋值。

*示例结束*

### 9.4.4.28 ! 表达式

对于形式如下的表达式 expr：

! expr_operand

- v 在 expr_operand 之前的确定赋值状态与 v 在 expr 之前的确定赋值状态相同。
- v 在 expr 之后的状态由以下各项确定：
  - 如果 v 在 expr_operand 之后的状态为确定已赋值，则 v 在 expr 之后的状态为确定已赋值。
  - 否则，如果 v 在 expr_operand 之后的状态为“假表达式后确定已赋值”，则 v 在 expr 之后的状态为“真表达式后确定已赋值”。
  - 否则，如果 v 在 expr_operand 之后的状态为“真表达式后确定已赋值”，则 v 在 expr 之后的状态为“假表达式后确定已赋值”。
  - 否则，v 在 expr 之后的状态不是确定已赋值。

### 9.4.4.29 ?? 表达式

对于形式如下的表达式 expr：

expr_first ?? expr_second

- v 在 expr_first 之前的确定赋值状态与 v 在 expr 之前的确定赋值状态相同。
- v 在 expr_second 之前的确定赋值状态与 v 在 expr_first 之后的状态相同。
- v 在 expr 之后的状态由以下各项确定：
  - 如果 expr_first 是值为 null 的常量表达式（§11.20），则 v 在 expr 之后的状态与 v 在 expr_second 之后的状态相同。
  - 否则，v 在 expr 之后的状态与 v 在 expr_first 之后的确定赋值状态相同。

### 9.4.4.30 ?: 表达式

对于形式如下的表达式 expr：

expr_cond ? expr_true : expr_false

- v 在 expr_cond 之前的确定赋值状态与 v 在 expr 之前的状态相同。
- 如果 v 在 expr_cond 之后的状态为确定已赋值或“真表达式后确定已赋值”，则 v 在 expr_true 之前的确定赋值状态为确定已赋值。
- 如果 v 在 expr_cond 之后的状态为确定已赋值或“假表达式后确定已赋值”，则 v 在 expr_false 之前的确定赋值状态为确定已赋值。
- v 在 expr 之后的状态由以下各项确定：
  - 如果 expr_cond 是值为 true 的常量表达式（§11.20），则 v 在 expr 之后的状态与 v 在 expr_true 之后的状态相同。

