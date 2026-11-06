# # Exercises

+   1. **10.6 (Memory Allocation and Deallocation Operators)**  
+      Compare and contrast dynamic memory allocation and deallocation operators `new`, `new []`, `delete` and `delete[]`.

+   2. **10.7 (Overloading the Parentheses Operator)** One nice example of overloading the function call operator `()` is to allow another form of double-array subscripting popular in some programming languages. Instead of saying

```
chessBoard[row][column]
```

for an array of objects, overload the function call operator to allow the alternate form

```
chessBoard(row, column)
```

Create a class `DoubleSubscriptedArray` that has similar features to class `Array` in **Figs. 10.10–10.11**. At construction time, the class should be able to create a `DoubleSubscriptedArray` of any number of rows and columns. The class should supply `operator()` to perform double-subscripting operations. For