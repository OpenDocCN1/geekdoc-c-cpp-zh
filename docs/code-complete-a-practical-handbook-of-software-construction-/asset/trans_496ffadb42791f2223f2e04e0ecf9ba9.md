

APL 更简单且不易出错。它仅使用三个操作数，而 Java 片段使用 17 个。它没有循环变量、数组索引或可能编码错误的控制结构。

此示例的一个要点是，你做一些编程来解决问题，还有一些编程来用特定语言解决它。你用来解决问题语言会极大地影响你的解决方案。

## CHECKLIST：循环

## 循环选择和创建
- 是否在适当的情况下使用 `while` 循环而不是 `for` 循环？
- 循环是否从内向外创建？

## 进入循环
- 循环是否从顶部进入？
- 初始化代码是否直接位于循环之前？
- 如果循环是无限循环或事件循环，是否干净地构造，而不是使用 `for i = 1 to 9999` 之类的权宜之计？
- 如果循环是 C++、C 或 Java `for` 循环，循环头是否保留用于循环控制代码？

## 循环内部
- 循环是否使用 `{` 和 `}` 或其等价物来包含循环体并防止因不当修改而产生的问题？
- 循环体中是否有内容？它是否非空？
- 家务处理是否在循环开始或结束时分组？
- 循环是否执行一个且仅一个功能，就像一个定义良好的例程一样？
- 循环是否足够短，可以一次全部查看？
- 循环嵌套是否不超过三层？
- 长的循环内容是否已移入其自己的例程？
- 如果循环很长，是否特别清晰？

## 循环索引
- 如果循环是 for 循环，其内部代码是否避免篡改循环索引？
- 是否使用变量来保存重要的循环索引值，而不是在循环外部使用循环索引？
- 循环索引是序数类型还是枚举类型——而不是浮点数？
- 循环索引是否有有意义的名称？
- 循环是否避免索引串扰？

## 退出循环
- 循环是否在所有可能条件下结束？
- 循环是否使用安全计数器——如果你已制定了安全计数器标准？
- 循环的终止条件是否明显？
- 如果使用 break 或 continue，它们是否正确？

## 关键点
- 循环很复杂。保持它们简单有助于阅读你代码的人。
- 保持循环简单的技术包括避免奇特的循环类型、最小化嵌套、使入口和出口清晰，以及将家务代码放在一个地方。
- 循环索引受到大量滥用。清晰地命名它们，并仅将其用于一个目的。
- 仔细思考循环，以验证它在每种情况下是否正常运行，并在所有可能条件下终止。

## 第 17 章

## 不寻常的控制结构

### 目录
- 17.1 例程的多重返回：页 391
- 17.2 递归：页 393
- 17.3 `goto`：页 398
- 17.4 不寻常控制结构的视角：页 408

### 相关主题
- 通用控制问题：第 19 章
- 直线代码：第 14 章
- 带有条件语句的代码：第 15 章
- 带有循环的代码：第 16 章
- 异常处理：第 8.4 节

一些控制结构存在于一种模糊的黄昏地带，同时处于领先边缘和被否定和证伪的状态——通常同时处于两者！这些结构并非在所有语言中都可用，但在提供它们的语言中，只要谨慎使用就可以有用。

## 17.1 例程的多重返回

大多数语言都支持某种从例程中途退出例程的手段。*return* 和 *exit* 语句是控制结构，使程序能够随时从例程退出。它们导致例程通过正常退出通道终止，将控制权返回给调用例程。这里的 *return* 一词用作 C++ 和 Java 中的 *return*、Microsoft Visual Basic 中的 *Exit Sub* 和 *Exit Function* 以及类似结构的通用术语。以下是使用 *return* 语句的指导原则：

![](img/649c8eee28c38ca1e062691e45dc9883_427_0.png)

**在提高可读性时使用 return**  在某些例程中，一旦你知道答案，就想立即将其返回给调用例程。如果例程定义为在检测到错误后不需要任何进一步清理，那么不立即返回意味着你必须编写更多代码。

以下是一个在例程中的多个位置返回是合理的良好示例：

此例程返回一个 Comparison 枚举类型。

### C++ 例程多重返回的良好示例

```
Comparison Compare( int value1, int value2 ) {
    if ( value1 < value2 ) {
        return Comparison_LessThan;
    }
    else if ( value1 > value2 ) {
        return Comparison_GreaterThan;
    }
    return Comparison_Equal;
}
```

其他示例就不那么明确了，如下一小节所示。

### 使用 guard clauses（提前返回或退出）简化复杂的错误处理

必须在执行其名义操作之前检查大量错误条件的代码可能导致深度缩进的代码并可能掩盖名义情况，如下所示：

这是名义情况的代码。

### 掩盖名义情况的 Visual Basic 代码

```
If file.validName() Then
    If file.Open() Then
        If encryptionKey.valid() Then
            If file.Decrypt( encryptionKey ) Then
                * lots of code
                ...
            End If
        End If
    End If
End If
```

将例程的主体缩进在四个 if 语句内部在美学上很丑陋，尤其是如果最内层的 if 语句内有大量代码。在这种情况下，如果先检查错误情况，为代码的正常路径扫清道路，代码的流程有时会更清晰。以下是它可能的样子：

### 使用 Guard Clauses 使名义情况更清晰的简单 Visual Basic 代码

```
* set up, bailing out if errors are found
If Not file.validName() Then Exit Sub
If Not file.Open() Then Exit Sub
If Not encryptionKey.valid() Then Exit Sub
If Not file.Decrypt( encryptionKey ) Then Exit Sub

* lots of code
...
```

这种简单代码使这种技术看起来像是一个整洁的解决方案，但生产代码在检测到错误条件时通常需要更广泛的家务处理或清理。以下是更现实的示例：

```
更现实的 Visual Basic 代码，使用 Guard Clauses 使名义情况更清晰
* set up, bailing out if errors are found
If Not file.validName() Then
    errorStatus = FileError_InvalidFileName
    Exit Sub
End If

If Not file.Open() Then
    errorStatus = FileError_CantOpenFile
    Exit Sub
End If

If Not encryptionKey.valid() Then
    errorStatus = FileError_InvalidEncryptionKey
    Exit Sub
End If

If Not file.Decrypt( encryptionKey ) Then
    errorStatus = FileError_CantDecryptFile
    Exit Sub
End If

* lots of code
...
```

这是名义情况的代码。

对于生产规模的代码，Exit Sub 方法在处理名义情况之前会产生大量代码。然而，Exit Sub 方法确实避免了第一个示例中的深度嵌套，而且，如果第一个示例中的代码扩展以显示设置 errorStatus 变量，Exit Sub 方法会更好地将相关语句保持在一起。尘埃落定后，Exit Sub 方法确实更具可读性和可维护性，只是优势并不大。

### 最小化每个例程中的返回次数

当阅读例程底部时，如果你不知道它可能在上方某个位置返回，就更难理解该例程。因此，谨慎使用返回——仅在它们提高可读性时使用。

## 17.2 递归

在递归中，例程自行解决问题的很小一部分，将问题分解为更小的部分，然后调用自身来解决每个较小的部分。当问题的很小部分很容易解决且很大部分很容易分解为更小的部分时，通常会使用递归。

递归并不经常有用，但在谨慎使用时它会产生优雅的解决方案，如在此示例中，排序算法很好地使用了递归：

![](img/649c8eee28c38ca1e062691e45dc9883_429_0.png)

