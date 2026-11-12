
如果 E 是前缀表达式，而 Y 是任何非空的非空白字符串，那么 E Y 不能是前缀表达式。这是一个微妙的点；本章末尾的练习 17 要求你证明这一点。

如果 E 是前缀表达式，E Y 不能是

基于这一观察，你可以通过观察第一个前缀表达式来开始确定是否有两个连续的前缀表达式。如果你找到了一个，前面的观察意味着这个第一个表达式只有一个可能的终点。

如果你发现第一个前缀表达式在位置 end1 处结束，你接着尝试在位置 end1 + 1 处查找第二个前缀表达式。如果你找到了第二个表达式，必须检查是否已到达所讨论字符串的末尾。

利用这些思想，你可以例如证明 +*ab-cd 是一个前缀表达式。要使 +*ab-cd 成为前缀表达式，它必须采用 +E1E2 的形式，其中 E1 和 E2 是前缀表达式。现在你可以写

- E1 = * E2 E4，其中
- E2 = a
- E4 = b

因为 E1 和 E4 是前缀表达式，所以 E1 是前缀表达式。同样，你可以写

- E2 = - E5 E6，其中
- E5 = c
- E6 = d

你可以看出 E2 是一个前缀表达式。

你可以编写一个函数来测试一个表达式是否为前缀表达式，方法是先构建一个递归值函数 endPre(strExp, first)，用于检查字符串 strExp 中从位置 first 开始的表达式，并定位其找到的第一个前缀表达式的结束位置。如果成功，该函数返回前缀表达式结束位置的索引。如果不存在这样的前缀表达式，endPre 返回 -1。该函数的伪代码如下。

### endPre 确定前缀表达式的结束位置

```
endPre(strExp: string, first: integer): integer
last = strExp.length() - 1
if (first < 0 or first > last)
return -1
ch = character at position first of strExp
if (ch is an identifier)
return first // Index of last character in simple prefix expression
else if (ch is an operator)
{
// Find the end of the first prefix expression
firstEnd = endPre(strExp, first + 1) // Point X
// If the end of the first prefix expression was found, find the end of the second
// prefix expression
if (firstEnd > -1)
return endPre(strExp, firstEnd + 1) // Point Y
else
return -1
}
else
return -1
```

图 5-3 包含了当初始表达式为 +*ab-cd 时 endPre 的跟踪。

### 图 5-3 endPre("+*ab-cd", 0) 的跟踪

进行初始调用 endPre("+*ab-cd", 0)，endPre 开始执行：

```
first last
= 0   = 6
```

strExp 的下一个字符是 +，因此在点 X 处进行递归调用，新的 endPre 调用开始执行：

```
first last   X       first last   X       first last
= 0   = 6      = 1   = 6      = 2   = 6
last = 6       last = 6
firstEnd = 7   firstEnd = 2
X.endPre(...)  X.endPre(...)  ?
```

strExp 的下一个字符是 *，因此在点 X 处进行递归调用，新的 endPre 调用开始执行：

```
first last   X       first last   X       first last
= 0   = 6      = 1   = 6      = 2   = 6
last = 6       last = 6
firstEnd = 7   firstEnd = 2
X.endPre(...)  X.endPre(...)  ?
```

strExp 的下一个字符是 a，这是一个基本情况。当前的 endPre 调用完成执行并返回其值：

```
first last   X       first last       first last
= 0   = 6      = 1   = 6      = 2   = 6
last = 6       last = 6       last = 6
firstEnd = 7   firstEnd = 2   return 2
X.endPre(...)  return 2
```

因为 firstEnd > -1，从点 Y 进行递归调用，新的 endPre 调用开始执行：

```
first last   X       first last       first last
= 0   = 6      = 1   = 6      = 3   = 6
last = 6       Y: endPre(...)  last
firstEnd = 7   Y: endPre(...)  return ?
X.endPre(...)  return ?
```

strExp 的下一个字符是 b，这是一个基本情况。当前的 endPre 调用完成执行并返回其值：

```
first last   X       first last       first last
= 0   = 6      = 1   = 6      = 3   = 6
last = 6       last = 6       last = 6
firstEnd = 7   firstEnd = 2   return 3
X.endPre(...)  return 3   return 3
```

当前的 endPre 调用完成执行并返回其值：

```
first last   X       first last
= 0   = 6      = 1   = 6
last = 6       last = 6
firstEnd = 3   firstEnd = 2
return 3       return 3
```

因为 firstEnd > -1，从点 Y 进行递归调用，新的 endPre 调用开始执行：

```
last firstEnd
= 6   = 3
first = 3
Y: endPre("+*ab-cd", 4)
return ?       first last
               = 4   = 6
               last = 6
```

strExp 的下一个字符是 -，因此在点 X 处进行递归调用，新的 endPre 调用开始执行：

![](img/288a0c22d14d2450c1e772f228f867b0_195_0.png)

strExp 的下一个字符是 c，这是一个基本情况。当前的 endPre 调用完成执行并返回其值：

![](img/288a0c22d14d2450c1e772f228f867b0_195_1.png)

因为 FirstEnd > -1，从点 Y 进行递归调用，新的 endPre 调用开始执行：

![](img/288a0c22d14d2450c1e772f228f867b0_195_2.png)

strExp 的下一个字符是 d，这是一个基本情况。当前的 endPre 调用完成执行并返回其值：

![](img/288a0c22d14d2450c1e772f228f867b0_195_3.png)

当前的 endPre 调用完成执行并返回其值：

![](img/288a0c22d14d2450c1e772f228f867b0_195_4.png)

当前的 endPre 调用完成执行并将其值返回给对 endPre 的原始调用：

![](img/288a0c22d14d2450c1e772f228f867b0_195_5.png)

现在你可以使用函数 endPre 来确定字符串是否包含前缀表达式，方法如下：

```
// See whether an expression is a prefix expression.
// Precondition: strExp contains a string with no blank characters.
// Postcondition: Returns true if the expression is in prefix form; otherwise returns false.
isPrefix(strExp: string): boolean
   lastChar = endPre(strExp, 0)
   return (lastChar >= 0) and (lastChar == strExp.length() - 1)
```

### 前缀表达式的识别算法

一旦确定一个字符串是前缀表达式，如何对其求值？因为每个运算符后面跟着它的两个操作数，你可以在表达式中向前查找它们。然而，这样的操作数本身也可以是前缀表达式，你必须先对它们求值。这些前缀表达式是原始表达式的子表达式，因此必须更“小”。这个问题的递归解决方案似乎很自然。

下面出现在伪代码中的函数对前缀表达式求值。这个算法比对中缀表达式求值的算法更简单。

### 计算前缀表达式的算法

```
// Returns the value of a given prefix expression.
// Precondition: strExp is a string containing a valid prefix expression with no blanks.
evaluatePrefix(strExp: string): Float
  strLength = the length of strExp
  if (strLength == 1)
    return value of the identifier // Base case--single identifier
  else
  {
    op = strExp[0] // strExp begins with an operator
    // Find the end of the first prefix expression--will be the first operand
    endFirst = endPre(strExp, 1)
    // Recursively evaluate this first prefix expression
    operand1 = evaluatePrefix(strExp[1..endFirst]);
    // Recursively evaluate the second prefix expression--will be the second operand
    endSecond = strLength - endFirst + 1
    operand2 = evaluatePrefix(strExp[endFirst + 1, endSecond])
    // Evaluate the prefix expression
    return operand1 op operand2
  }
```

- **问题 2** 写出表示以下中缀表达式的前缀表达式：`(a/b) * c-(d + e) * f`
- **问题 3** 写出表示以下前缀表达式的中缀表达式：`-a/b + c * def`
- **问题 4** 以下字符串是前缀表达式吗？`+- /abc * + def * gh`

## 5.2.3 后缀表达式

定义所有后缀表达式语言的语法是

```
<postfix> = <identifier>|<postfix><postfix><operator>
<operator> = + | -|*|
<identifier> = a | b | ... | z
```

有些计算器要求你在输入要执行的运算之前先输入两个数字。事实上，这样的计算器要求你输入后缀表达式。

这里我们将开发一个将前缀表达式转换为后缀表达式的算法。第 6 章介绍了一个对后缀表达式求值的非递归算法。这两个算法共同为你提供了另一种计算前缀表达式的技术。为了简化转换算法，假设通过使用前缀识别算法，你拥有一个语法正确的前缀表达式。

如果你以递归方式思考，从前缀形式到后缀形式的转换是简单直接的。如果前缀表达式 exp 是一个单个字母，那么

```
postfix(exp) = exp
```
