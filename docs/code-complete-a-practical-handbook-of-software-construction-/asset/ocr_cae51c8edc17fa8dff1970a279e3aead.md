short fragment. The next example shows how to reduce that number to only three elements within each block of code:

# C++ Example of Using Two Sets of Variables More Understandably

```
void SummarizeData( ... ) {
  GetOldData( oldData, &numOldData );
  totalOldData = Sum( oldData, numOldData );
  PrintOldDataSummary( oldData, totalOldData, numOldData );
  SaveOldDataSummary( totalOldData, numOldData );
  ...
  GetNewData( newData, &numNewData );
  totalNewData = Sum( newData, numNewData );
  PrintNewDataSummary( newData, totalNewData, numNewData );
  SaveNewDataSummary( totalNewData, numNewData );
  ...
}
```

Statements using oldData.

Statements using newData.

When the code is broken up, the two blocks are each shorter than the original block and individually contain fewer variables. They’re easier to understand, and if you need to break this code out into separate routines, the shorter blocks with fewer variables will promote better-defined routines.

# Break groups of related statements into separate routines

All other things being equal, a variable in a shorter routine will tend to have smaller span and live time than a variable in a longer routine. By breaking related statements into separate, smaller routines, you reduce the scope that the variable can have.

> Cross-Reference For more on global variables, see Section 13.3, “Global Data.”

# Begin with most restricted visibility, and expand the variable’s scope only if necessary

Part of minimizing the scope of a variable is keeping it as local as possible. It is much more difficult to reduce the scope of a variable that has had a large scope than to expand the scope of a variable that has had a small scope—in other words, it’s harder to turn a global variable into a class variable than it is to turn a class variable into a global variable. It’s harder to turn a protected data member into a private data member than vice versa. For that reason, when in doubt, favor the smallest possible scope for a variable: local to a specific loop, local to an individual routine, then private to a class, then protected, then package (if your programming language supports that), and global only as a last resort.

# Comments on Minimizing Scope

Many programmers’ approach to minimizing variables’ scope depends on their views of the issues of “convenience” and “intellectual manageability.” Some programmers make many of their variables global because global scope makes variables convenient to access and the programmers don’t have to fool around with parameter lists and class-scoping rules. In their minds, the convenience of being able to access variables at any time outweighs the risks involved.