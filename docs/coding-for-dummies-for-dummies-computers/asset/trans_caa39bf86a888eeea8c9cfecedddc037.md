
**表9-2——常见 JavaScript 运算符**

| 类型 | 运算符 | 描述 | 示例 |
|---|---|---|---|
| 小于 | `<` | 判断一个值是否小于另一个值 | `(x < 55)` |
| 大于 | `>` | 判断一个值是否大于另一个值 | `(x > 55)` |
| 相等 | `===` | 判断两个值是否相等 | `(x === 55)` |
| 小于或等于 | `<=` | 判断一个值是否小于或等于另一个值 | `(x <= 55)` |
| 大于或等于 | `>=` | 判断一个值是否大于或等于另一个值 | `(x >= 55)` |
| 不相等 | `!=` | 判断两个值是否不相等 | `(x != 55)` |

这里是一个简单的 `if` 语句，不包含 `else`：

```javascript
var carSpeed = 70;
if (carSpeed > 55) {
    alert("You are over the speed limit!");
}
```

在这个语句中，我声明一个名为 `carSpeed` 的变量，并将其设为 70。然后，一个带条件的 `if` 语句会比较变量 `carSpeed` 中的值是否大于 55。如果条件为真，则一个警告框（即弹出框）会显示“您已超速！”（参见图9-3。）在此例中，`carSpeed` 的值为 70，大于 55，因此条件为真，并显示警告框。如果第一行代码改为 `var carSpeed = 40;`，那么条件为假，因为 40 小于 55，不会显示任何警告框。

![](img/5a907eb39993e80f28c82efc2e4632b3_154_0.png)

**图9-3：** 警告弹出框。

让我们通过添加 `else` 来扩展 `if` 语句，创建 `if-else`，如下代码所示：

```javascript
var carSpeed = 40;
if (carSpeed > 55) {
    alert("You are over the speed limit!");
}
else {
    alert("You are under the speed limit!");
}
```

除了 `else` 之外，我还在 `else` 后面的花括号内添加了一个 `alert` 语句，并将 `carSpeed` 设为 40。当这个 `if-else` 语句执行时，`carSpeed` 等于 40，小于 55，因此条件为假；并且由于添加了 `else`，会弹出一个警告框，显示“您低于限速！”如果第一行代码改为 `var carSpeed = 70;`，如前所述，那么条件为真，因为 70 大于 55，将显示第一个警告框。

当前的 `if-else` 语句允许我们测试一个条件，并根据条件为真或假显示不同结果。要测试两个或更多条件，可以在原来的 `if` 语句后添加一个或多个 `else if` 语句。其一般语法如下：

```
if (condition1) {
    statement1 to execute if condition1 is true
}
else if (condition2) {
    statement2 to execute if condition2 is true
}
else {
    statement3 to execute if all previous conditions are false
}
```

`if-else` 的写法与前面一样，`else if` 后跟一个空格，然后是一个括在圆括号中的条件，该条件的求值结果为真或假。如果 `condition1` 为真，则执行位于第一组花括号之间的 `statement1`。如果 `condition1` 为假，则对 `condition2` 求值，并判断其结果为真或假。如果 `condition2` 为真，则执行位于第二组花括号之间的 `statement2`。此时，可以添加更多 `else if` 语句来测试更多条件。只有当所有 `if` 和 `else if` 条件都为假，并且包含 `else` 时，才会执行 `statement3`。在一个代码块中只会执行一个语句，之后其余语句会被忽略，并执行下一个代码块。

![](img/5a907eb39993e80f28c82efc2e4632b3_156_0.png)

编写 `if-else` 时，必须有一个且只能有一个 `if` 语句；如果选择使用，则必须有一个且只能有一个 `else` 语句。`else if` 是可选的，可以在单个 `if-else` 语句中使用多次，并且必须位于原来的 `if` 语句之后、`else` 之前。不能在没有前面的 `if` 语句的情况下单独使用 `else if` 或 `else`。

以下是另一个 `else if` 语句的示例：

```javascript
var carSpeed = 40;
if (carSpeed > 55) {
    alert("You are over the speed limit!");
}
else if (carSpeed === 55) {
    alert("You are at the speed limit!");
}
```

当这个 `if` 语句执行时，`carSpeed` 等于 40，小于 55，因此条件为假，然后对 `else if` 条件求值。`carSpeed` 的值并不完全等于 55，所以这个条件也为假，不会显示任何类型的警告框，语句到此结束。如果第一行代码改为 `var carSpeed = 55;`，那么第一个条件为假，因为 55 不大于 55。然后对 `else if` 条件求值，由于 55 正好等于 55，会显示第二个警告框，显示“您正好达到限速！”

![](img/5a907eb39993e80f28c82efc2e4632b3_156_1.png)

仔细看上面的代码——给变量赋值时使用一个等号，而比较两个值是否相等时，则使用三个等号（`===`）。

作为最后一个示例，下面是一个包含 `else if` 语句的 `if-else` 语句：

```javascript
var carSpeed = 40;
if (carSpeed > 55) {
    alert("You are over the speed limit!");
}
else if (carSpeed === 55) {
    alert("You are at the speed limit!");
}
else {
    alert("You are under the speed limit!");
}
```

如图9-4中的图所示，两个条件（在图中显示为菱形）会按顺序求值。在此示例中，`carSpeed` 等于 40，因此两个条件都为假，并执行 `else` 后面的语句，显示一个警告框，内容为“您低于限速！”这里 `carSpeed` 最初设为 40，但根据 `carSpeed` 变量的初始值，可能会显示三个警告框中的任意一个。

![](img/5a907eb39993e80f28c82efc2e4632b3_157_0.png)

**图9-4：** 包含 `else if` 语句的 if-else。

![](img/5a907eb39993e80f28c82efc2e4632b3_157_1.png)

条件总是先求值，并且每个条件必须是*真*或*假*。与条件无关的是当条件为真时执行的语句。

## 使用字符串和数字方法

最基本的数据类型通常存储在变量中，即字符串和数字。程序员经常需要操作字符串和数字来执行如下基本任务：

- 确定字符串的*长度*，例如用于密码。
- 选择字符串的一部分（或*子字符串*），例如在包含名和姓的字符串中选择名字。
- 将数字四舍五入到*固定*的小数点位数，例如在在线购物车中计算小计、计算税费、将税费四舍五入到两位小数，并将税费加到小计中。

这些任务非常常见，因此 JavaScript 包含了称为*方法*的快捷方式（在上文中以斜体显示），使执行这类任务更加容易。执行这些任务的一般语法是，在受影响的变量名或值后面跟一个句点和该方法名，如下所示（分别用于值和变量）：

```
value.method;
variable.method;
```

*表9-3* 展示了用于上述基本任务的 JavaScript 方法示例。示例包括应用于值（如字符串）的方法，以及应用于变量的方法。

**表9-3——常见 JavaScript 方法**

| 方法 | 描述 | 示例 | 结果 |
|---|---|---|---|
| `.toFixed(n)` | 将数字四舍五入到 *n* 位小数 | `var jenny = 8.675309;`<br>`jenny.toFixed(2);` | `8.68` |
| `.length` | 表示字符串中的字符数 | `"Nik".length;` | `3` |
| `.substring(start, end)` | 提取字符串从位置 start 到 end 的一部分。位置指每个字符之间的位置，并从第一个字符之前以零开始。 | `var name = "Inbox";`<br>`name.substring(2,5);` | `box` |

![](img/5a907eb39993e80f28c82efc2e4632b3_158_0.png)

使用字符串，或将变量赋值为字符串时，始终要用引号将字符串括起来。

`.toFixed` 和 `.length` 方法相对简单，但 `.substring` 方法可能有点令人困惑。`.substring(start, end)` 中使用的起始位置和结束位置并不指实际字符，而是指每个字符之间的空隙。图9-5展示了起始位置和结束位置如何工作。语句 `"Inbox".substring(2,5)` 从位置 2 开始，即 "n" 和 "b" 之间，到位置 5 结束，即 "x" 之后。

![](img/5a907eb39993e80f28c82efc2e4632b3_158_1.png)

*图9-5。* `.substring` 方法引用的是字符串中字符之间的位置。
