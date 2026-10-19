
**Cross-Reference** Retesting part of the condition to reduce complexity is similar to retesting a status variable. That technique is demonstrated in “Error Processing and gotos” in Section 17.3.

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

This example is contrived to show nesting levels. The // *lots of code* parts are intended to suggest that the routine has enough code to stretch across several screens or across the page boundary of a printed code listing. Here’s the code revised to use retesting rather than nesting:

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

This is a particularly realistic example because it shows that you can’t reduce the nesting level for free; you have to put up with a more complicated test in return for the reduced level of nesting. A reduction from four levels to two is a big improvement in readability, however, and is worth considering.

***Simplify a nested if by using a break block***  An alternative to the approach just described is to define a section of code that will be executed as a block. If some condition in the middle of the block fails, execution skips to the end of the block.

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

This technique is uncommon enough that it should be used only when your entire team is familiar with it and when it has been adopted by the team as an accepted coding practice.

*Convert a nested if to a set of if-then-elses*  If you think about a nested if test critically, you might discover that you can reorganize it so that it uses if-then-elses rather than nested ifs. Suppose you have a bushy decision tree like this:

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

This test is poorly organized in several ways, one of which is that the tests are redundant. When you test whether quantity is greater than 1000, you don’t also need to test whether it’s greater than 100 and greater than 10. Consequently, you can reorganize the code:

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

This solution is easier than some because the numbers increase neatly. Here’s how you could rework the nested if if the numbers weren’t so tidy:

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

The main difference between this code and the previous code is that the expressions in the else-if clauses don’t rely on previous tests. This code doesn’t need the else clauses to work, and the tests actually could be performed in any order. The code could consist of four ifs and no elses. The only reason the else version is preferable is that it avoids repeating tests unnecessarily.

## Convert a nested if to a case statement

You can recode some kinds of tests, particularly those with integers, to use a case statement rather than chains of ifs and elses. You can’t use this technique in some languages, but it’s a powerful technique for those in which you can. Here’s how to recode the example in Visual Basic:

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

This example reads like a book. When you compare it to the two examples of multiple indentations a few pages earlier, it seems like a particularly clean solution.

***Factor deeply nested code into its own routine***  If deep nesting occurs inside a loop, you can often improve the situation by putting the inside of the loop into its own routine. This is especially effective if the nesting is a result of both conditionals and iterations. Leave the *if-then-else* branches in the main loop to show the decision branching, and then move the statements within the branches to their own routines. This code needs to be improved by such a modification:

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

The code in the new routines has simply been lifted out of the original routine and formed into new routines. (The new routines aren’t shown here.) The new code has several advantages. First, two-level nesting makes the structure simpler and easier to understand. Second, you can read, modify, and debug the shorter while loop on one screen—it doesn’t need to be broken across screen or printed-page boundaries. Third, putting the functionality of ProcessDeposit() and ProcessWithdrawal() into routines accrues all the other general advantages of modularization. Fourth, it’s now easy to see that the code could be broken into a case statement, which would make it even easier to read, as shown below:

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
