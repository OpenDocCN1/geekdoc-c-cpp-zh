

这种声明变量的风格并不罕见，但由于所有声明都挤在一起，变量仍然很难找到，变量的类型也同样难以找到。现在，在代码清单 31-54 中，`nextColor` 的类型是什么？

## 代码清单 31-54　C++ 示例：通过每行只放一个变量声明提高可读性

```
int rowIndex;
int columnIdx;
Color previousColor;
Color currentColor;
Color nextColor;
Point previousTop;
Point previousBottom;
Point currentTop;
Point currentBottom;
Point nextTop;
Point nextBottom;
Font previousTypeface;
Font currentTypeface;
Font nextTypeface;
Color choices[ NUM_COLORS ];
```

与代码清单 31-53 中的 `nextTypeface` 相比，`nextColor` 变量在代码清单 31-54 中可能更容易找到。这种风格的特点是每行只声明一个变量，并且每行都包含完整的声明，包括变量类型。

诚然，这种风格会占用大量屏幕空间——从第一个示例的 3 行变成了 20 行，尽管那 3 行也确实很难看。我举不出任何研究表明这种风格会减少缺陷或提高理解力。不过，如果初级程序员萨莉（Sally Programmer, Jr.）请我评审她的代码，而她的数据声明看起来像第一个示例，我会说：“没门——太难读了。”如果看起来像第二个示例，我会说：“呃……也许我回头再答复你。”如果看起来像最后一个示例，我会说：“当然可以——这是我的荣幸。”

在变量首次使用的位置附近声明变量。与把所有变量集中在一个大块中声明相比，更可取的风格是将每个变量声明在它首次使用的位置附近。这样可以缩短“跨度”和“存活时间”，并在必要时便于将代码重构为更小的例程。更多细节参见 10.4 节“尽可能缩短变量的‘存活’时间”。

合理地排列声明。在代码清单 31-54 中，声明按类型分组。按类型分组通常是合理的，因为相同类型的变量往往会在相关操作中使用。在其他情况下，你也可以选择按变量名的字母顺序排列。虽然字母顺序排列有很多支持者，但我的感觉是，这样做太费力，得不偿失。如果你的变量列表长到需要按字母顺序排列才能有所帮助，那么你的例程可能太大了。应该把它拆分成更小、变量更少的例程。

## 在 C++ 中，将星号放在指针声明的变量名旁边，或者声明指针类型

常见的指针声明会把星号放在类型旁边，如代码清单 31-55 所示：

### 代码清单 31-55　C++ 示例：指针声明中的星号

```
EmployeeList* employees;
File* inputFile;
```

把星号放在类型名旁边而不是变量名旁边的问题是：当你在一行中放多个声明时，星号只会作用于第一个变量，尽管视觉格式让人觉得它作用于该行的所有变量。你可以通过将星号放在变量名旁边而不是类型名旁边来避免这个问题，如代码清单 31-56 所示：

### 代码清单 31-56　C++ 示例：在指针声明中使用星号

```
EmployeeList *employees;
File *inputFile;
```

这种方法的弱点在于，它会让人觉得星号是变量名的一部分，但实际上并非如此。该变量既可以在带星号的情况下使用，也可以在不带星号的情况下使用。

最好的做法是声明一个指针类型，然后使用该类型。示例如代码清单 31-57 所示：

### 代码清单 31-57　C++ 示例：在声明中良好地使用指针类型

```
EmployeeListPointer employees;
FilePointer inputFile;
```

这种方法所针对的具体问题，可以通过要求所有指针都使用指针类型声明（如代码清单 31-57 所示）来解决，也可以通过要求每行不超过一个变量声明来解决。一定要至少采用其中一种解决方案！

## 31.6　注释的布局

> 交叉参考：关于注释其他方面的细节，参见第 32 章“自文档化代码”。

注释写得好可以大大提高程序的可读性；注释写得不好实际上反而会损害可读性。注释的布局在很大程度上决定了它们是有助于还是妨碍可读性。

## 将注释与对应代码一起缩进

视觉缩进是理解程序逻辑结构的重要辅助手段，好的注释不应干扰这种视觉缩进。例如，代码清单 31-58 所示例程的逻辑结构是什么？

### 代码清单 31-58　Visual Basic 示例：注释缩进不当

![](img/649c8eee28c38ca1e062691e45dc9883_800_0.png)

```
For transactionId = 1 To totalTransactions
* get transaction data
    GetTransactionType( transactionType )
    GetTransactionAmount( transactionAmount )
* process transaction based on transaction type
    If transactionType = Transaction_Sale Then
        AcceptCustomerSale( transactionAmount )
    Else
        If transactionType = Transaction_CustomerReturn Then
* either process return automatically or get manager approval, if required
            If transactionAmount >= MANAGER_APPROVAL_LEVEL Then
* try to get manager approval and then accept or reject the return
* based on whether approval is granted
                GetMgrApproval( isTransactionApproved )
                If ( isTransactionApproved ) Then
                    AcceptCustomerReturn( transactionAmount )
                Else
                    RejectCustomerReturn( transactionAmount )
                End If
            Else
* manager approval not required, so accept return
                AcceptCustomerReturn( transactionAmount )
            End If
        End If
    End If
Next
```

在这个示例中，你很难看出逻辑结构，因为注释完全掩盖了代码的视觉缩进。你可能很难相信会有人刻意决定使用这种缩进风格，但我在专业程序中见过这种写法，而且我知道至少有一本教科书推荐这种风格。

代码清单 31-59 中的代码与代码清单 31-58 中的完全相同，只是注释的缩进不同。

### 代码清单 31-59　Visual Basic 示例：注释缩进得当

```
For transactionId = 1 To totalTransactions
  * get transaction data
  GetTransactionType( transactionType )
  GetTransactionAmount( transactionAmount )

  * process transaction based on transaction type
  If transactionType = Transaction_Sale Then
    AcceptCustomerSale( transactionAmount )

  Else
    If transactionType = Transaction_CustomerReturn Then

      * either process return automatically or get manager approval, if required
      If transactionAmount >= MANAGER_APPROVAL_LEVEL Then

        * try to get manager approval and then accept or reject the return
        * based on whether approval is granted
        GetMgrApproval( isTransactionApproved )
        If ( isTransactionApproved ) Then
          AcceptCustomerReturn( transactionAmount )
        Else
          RejectCustomerReturn( transactionAmount )
        End If
      Else
        * manager approval not required, so accept return
        AcceptCustomerReturn( transactionAmount )
      End If
    End If
  End If
Next
```

在代码清单 31-59 中，逻辑结构更加明显。一项关于注释有效性的研究发现，注释的益处并不确定，作者推测这是因为注释“干扰了对程序的视觉扫描”（Shneiderman, 1980）。从这些例子可以明显看出，注释的风格强烈影响着注释是否会造成干扰。

## 用至少一个空行将每条注释分隔开

如果有人想对程序有个整体了解，最有效的方式是不读代码，只读注释。用空行把注释分隔开，有助于读者浏览代码。示例如代码清单 31-60 所示：

### 代码清单 31-60　Java 示例：用空行将注释分隔开

```
// comment zero
CodeStatementZero;
CodeStatementOne;

// comment one
CodeStatementTwo;
CodeStatementThree;
```

