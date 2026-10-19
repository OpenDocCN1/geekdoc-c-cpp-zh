

**交叉引用** 重新测试部分条件以降低复杂度与重新测试状态变量类似。该技术在第 17.3 节“错误处理和 goto”中有所演示。

```cpp
// lots of code
---
if ( SetupPage() ) {
    // lots of code
    ---
    if ( AllocMem( &printData ) ) {
        // lots of code
        ---
    }
}
}
}
```

此示例是为了展示嵌套层级而构造的。// *lots of code* 部分旨在暗示该例程的代码量足以跨越数个屏幕或跨越打印代码列表的页面边界。以下是修改为使用重新测试而非嵌套的代码：

```cpp
**C++ Example of Code Mercifully Unnested by Retesting**
if ( inputStatus == InputStatus_Success ) {
    // lots of code
    ---
    if ( printerRoutine != NULL ) {
        // lots of code
        ---
    }
}

if ( ( inputStatus == InputStatus_Success ) &&
     ( printerRoutine != NULL ) && SetupPage() ) {
    // lots of code
    ---
    if ( AllocMem( &printData ) ) {
        // lots of code
        ---
    }
}
```

这是一个特别现实的示例，因为它表明你不能免费降低嵌套层级；为了换取降低的嵌套层级，你必须忍受更复杂的测试。然而，从四层减少到两层的改进对可读性来说是巨大的提升，值得考虑。

***通过使用 break 块简化嵌套 if***  另一种替代方法是在描述中定义一段将作为块执行的代码。如果块中间的某个条件失败，执行将跳到块的末尾。

```cpp
**C++ Example of Using a break Block**
do {
    // begin break block
    if ( inputStatus != InputStatus_Success ) {
        break; // break out of block
    }
```

```
// lots of code
...
if ( printerRoutine == NULL ) {
    break; // break out of block
}

// lots of code
...
if ( !SetupPage() ) {
    break; // break out of block
}

// lots of code
...
if ( !AllocMem( &printData ) ) {
    break; // break out of block
}

// lots of code
...
} while (FALSE); // end break block
```

这种技术不常见，只有当你的整个团队熟悉它并且团队已将其作为公认的编码实践采纳时才应使用。

*将嵌套 if 转换为一组 if-then-else*  如果你批判性地思考嵌套 if 测试，你可能会发现可以将其重新组织以使用 if-then-else 而不是嵌套 if。假设你有如下的繁茂决策树：

```
Java Example of an Overgrown Decision Tree
if ( 10 < quantity ) {
    if ( 100 < quantity ) {
        if ( 1000 < quantity ) {
            discount = 0.10;
        }
        else {
            discount = 0.05;
        }
    }
    else {
        discount = 0.025;
    }
}
else {
    discount = 0.0;
}
```

此测试在多方面组织不佳，其中之一是测试是冗余的。当你测试 quantity 是否大于 1000 时，你不需要再测试它是否大于 100 且大于 10。因此，你可以重新组织代码：

```
Java Example of a Nested if Converted to a Set of if-then-elses
if ( 1000 < quantity ) {
    discount = 0.10;
}
else if ( 100 < quantity ) {
    discount = 0.05;
}
else if ( 10 < quantity ) {
    discount = 0.025;
}
else {
    discount = 0;
}
```

这个解决方案之所以更容易，是因为数字整齐递增。以下是数字不那么整齐时如何重写嵌套 if 的示例：

```
Java Example of a Nested if Converted to a Set of if-then-elses When the Numbers Are "Messy"
if ( 1000 < quantity ) {
    discount = 0.10;
}
else if ( ( 100 < quantity ) && ( quantity <= 1000 ) ) {
    discount = 0.05;
}
else if ( ( 10 < quantity ) && ( quantity <= 100 ) ) {
    discount = 0.025;
}
else if ( quantity <= 10 ) {
    discount = 0;
}
```

这段代码与前一段代码的主要区别在于 else-if 子句中的表达式不依赖于之前的测试。这段代码不需要 else 子句也能工作，并且测试实际上可以按任意顺序执行。代码可以由四个 if 组成且没有 else。else 版本更可取的唯一原因是它避免了不必要的重复测试。

## 将嵌套 if 转换为 case 语句

你可以用 case 语句重新编码某些类型的测试，特别是那些使用整数的测试，而不是使用 if 和 else 的链。你不能在某些语言中使用这种技术，但在可以使用的语言中它是一种强大的技术。以下是 Visual Basic 中重新编码示例的方法：

```
Visual Basic Example of Converting a Nested if to a case Statement
Select Case quantity
    Case 0 To 10
        discount = 0.0
    Case 11 To 100
        discount = 0.025
```

```vb
Case 101 To 1000
    discount = 0.05
Case Else
    discount = 0.10
End Select
```

这个示例读起来像一本书。当你将其与几页前多个缩进的两个示例进行比较时，它似乎是一个特别干净的解决方案。

***将深度嵌套的代码分解为自己的例程***  如果深度嵌套发生在循环内部，你通常可以通过将循环内部部分放入自己的例程来改善这种情况。如果嵌套是由于条件和迭代共同造成的，这种方法尤其有效。保留主循环中的 *if-then-else* 分支以显示决策分支，然后将分支内的语句移至其自己的例程。以下代码需要通过此类修改来改进：

```cpp
C++ Example of Nested Code That Needs to Be Broken into Routines
while ( !TransactionsComplete() ) {
    // read transaction record
    transaction = ReadTransaction();

    // process transaction depending on type of transaction
    if ( transaction.Type == TransactionType_Deposit ) {
        // process a deposit
        if ( transaction.AccountType == AccountType_Checking ) {
            if ( transaction.AccountSubType == AccountSubType_Business )
                MakeBusinessCheckDep( transaction.AccountNum, transaction.Amount );
            else if ( transaction.AccountSubType == AccountSubType_Personal )
                MakePersonalCheckDep( transaction.AccountNum, transaction.Amount );
            else if ( transaction.AccountSubType == AccountSubType_School )
                MakeSchoolCheckDep( transaction.AccountNum, transaction.Amount );
        }
        else if ( transaction.AccountType == AccountType_Savings )
            MakeSavingsDep( transaction.AccountNum, transaction.Amount );
        else if ( transaction.AccountType == AccountType_DebitCard )
            MakeDebitCardDep( transaction.AccountNum, transaction.Amount );
        else if ( transaction.AccountType == AccountType_MoneyMarket )
            MakeMoneyMarketDep( transaction.AccountNum, transaction.Amount );
        else if ( transaction.AccountType == AccountType_Cd )
            MakeCDDep( transaction.AccountNum, transaction.Amount );
    }
    else if ( transaction.Type == TransactionType_Withdrawal ) {
        // process a withdrawal
        if ( transaction.AccountType == AccountType_Checking )
            MakeCheckingWithdrawal( transaction.AccountNum, transaction.Amount );
        else if ( transaction.AccountType == AccountType_Savings )
            MakeSavingsWithdrawal( transaction.AccountNum, transaction.Amount );
        else if ( transaction.AccountType == AccountType_DebitCard )
            MakeDebitCardWithdrawal( transaction.AccountNum, transaction.Amount );
    }
}
```

新例程中的代码只是从原始例程中提取出来并形成新的例程。 （此处未显示新例程。）新代码有几个优点。首先，两级嵌套使结构更简单、更容易理解。其次，你可以在一个屏幕上阅读、修改和调试较短的 while 循环——它不需要跨越屏幕或打印页边界。第三，将 ProcessDeposit() 和 ProcessWithdrawal() 的功能放入例程中获得了模块化的所有其他一般优势。第四，现在很容易看出代码可以被分解为 case 语句，这将使其更易于阅读，如下所示：

## C++ Example of Good, Nested Code After Decomposition and Use of a case Statement

```
while ( !TransactionsComplete() ) {
    // read transaction record
    transaction = ReadTransaction();

    // process transaction depending on type of transaction
    switch ( transaction.Type ) {
        case ( TransactionType_Deposit ):
            ProcessDeposit(
                transaction.AccountType,
                transaction.AccountSubType,
                transaction.AccountNum,
                transaction.Amount
            );
            break;

        case ( TransactionType_Withdrawal ):
            ProcessWithdrawal(
                transaction.AccountType,
                transaction.AccountNum,
                transaction.Amount
            );
            break;

        case ( TransactionType_Transfer ):
            MakeFundsTransfer(
                transaction.SourceAccountType,
                transaction.TargetAccountType,
                transaction.AccountNum,
                transaction.Amount
            );
            break;

        default:
            // process unknown transaction type
            LogTransactionError("Unknown Transaction Type", transaction );
            break;
    }
}
```
