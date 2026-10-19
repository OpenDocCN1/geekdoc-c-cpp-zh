

```
if ( !( expression ) ) {
    break;
}

// do something
...
}
```

## 何时使用 for 循环

进一步阅读 有关使用 for 循环的更多良好准则，请参阅《编写坚实的代码》（Maguire 1993）。

当你需要一个执行指定次数的循环时，for 循环是一个不错的选择。你可以在 C++、C、Java、Visual Basic 和大多数其他语言中使用 for。

对于不需要内部循环控制的简单活动，使用 for 循环。当循环控制涉及简单的递增或简单的递减时使用它们，例如遍历容器中的元素。for 循环的要点是你在循环顶部设置好它，然后就忘记它。你不需要在循环内部做任何事情来控制它。如果存在需要跳出循环的条件，请改用 while 循环。

同样，不要显式更改 for 循环的索引值来强制其终止。改用 while 循环。for 循环适用于简单用途。大多数复杂的循环任务更适合由 while 循环处理。

## 何时使用 foreach 循环

foreach 循环或其等价形式（C# 中的 foreach，Visual Basic 中的 For-Each，Python 中的 for-in）对于对数组或其他容器的每个成员执行操作非常有用。它的优点是消除了循环维护算术运算，从而消除了循环维护算术运算中出现错误的可能性。以下是这种循环的示例：

```
C# Example of a foreach Loop
int [] fibonacciSequence = new int [] { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
int oddFibonacciNumbers = 0;
int evenFibonacciNumbers = 0;

// count the number of odd and even numbers in a Fibonacci sequence
foreach ( int fibonacciNumber in fibonacciSequence ) {
    if ( fibonacciNumber % 2 == 0 ) {
        evenFibonacciNumbers++;
    }
    else {
        oddFibonacciNumbers++;
    }
}

Console.WriteLine( "Found {0} odd numbers and {1} even numbers.",
    oddFibonacciNumbers, evenFibonacciNumbers );
```

## 使用 while( true ) 实现无限循环

你可能有一个不终止运行的循环——例如，固件中的循环，如心脏起搏器或微波炉。或者你可能有一个仅在响应事件时才终止的循环——“事件循环”。你可以用多种方式编写这种无限循环。用类似 for i = 1 to 99999 的语句伪造无限循环是一个糟糕的选择，因为特定的循环限制模糊了循环的意图——99999 可能是合法值。这种伪无限循环在维护时也可能失效。

while( true ) 惯用法被认为是在 C++、Java、Visual Basic 和其他支持类似结构的语言中编写无限循环的标准方法。一些程序员更喜欢使用 for( ; ; )，这是一种被接受的替代方案。

## 在适当时优先使用 for 循环

for 循环将循环控制代码打包在一个地方，这使得循环易于阅读。当修改软件时，程序员常犯的一个错误是在 while 循环顶部更改循环初始化代码，却忘记更改底部的相关代码。在 for 循环中，所有相关代码都在循环顶部集中在一起，这使得正确的修改更容易。如果可以适当使用 for 循环而不是其他类型的循环，就使用它。

## 不要在 while 循环更合适时使用 for 循环

在 C++、C# 和 Java 中，灵活的 for 循环结构的一个常见滥用是将 while 循环的内容随意塞进 for 循环头部。以下示例展示了 while 循环被塞进 for 循环头部的情况：

![](img/649c8eee28c38ca1e062691e45dc9883_410_0.png)

### C++ Example of a while Loop Abusively Crammed into a for Loop Header

```
// read all the records from a file
for ( inputFile.MoveToStart(), recordCount = 0; !inputFile.EndOfFile();
    recordCount++ ) {
    inputFile.GetRecord();
}
```

C++ 的 for 循环相对于其他语言中的 for 循环的优势在于它对初始化和终止信息可以使用的类型更灵活。这种灵活性固有的弱点是，你可以将与控制循环无关的语句放入循环头部。

将 for 循环头部保留给循环控制语句——初始化循环、终止循环或使其趋向终止的语句。在刚才显示的示例中，循环体中的 inputFile.GetRecord() 语句使循环趋向终止，但 recordCount 语句不这样做；它们是与控制循环进度无关的维护语句。将 recordCount 语句放入循环头部而将 inputFile.GetRecord() 语句排除在外会产生误导；它造成了 recordCount 控制循环的错误印象。

如果你想在这种情况下使用 for 循环而不是 while 循环，请将循环控制语句放入循环头部，其余全部排除。以下是正确使用循环头部的方法：

```
C++ Example of Logical if Unconventional Use of a for Loop Header
recordCount = 0;
for ( inputFile.MoveToStart(); !inputFile.EndOfFile(); inputFile.GetRecord() ) {
    recordCount++;
}
```

此示例中循环头部的内容都与循环控制相关。inputFile.MoveToStart() 语句初始化循环，!inputFile.EndOfFile() 语句测试循环是否已完成，inputFile.GetRecord() 语句使循环趋向终止。影响 recordCount 的语句不会直接使循环趋向终止，适当地未包含在循环头部。while 循环对于这项工作可能仍然更合适，但至少这段代码逻辑地使用了循环头部。顺便说一下，以下是使用 while 循环时代码的写法：

```
C++ Example of Appropriate Use of a while Loop
// read all the records from a file
inputFile.MoveToStart();
recordCount = 0;
while ( !inputFile.EndOfFile() ) {
    inputFile.GetRecord();
    recordCount++;
}
```

## 处理循环中间部分

以下小节描述了如何处理循环中间部分：

使用 { 和 } 来括起循环中的语句 每次都使用代码大括号。它们在运行时不会花费速度或空间，它们有助于可读性，并且有助于在代码被修改时防止错误。它们是一种良好的防御性编程实践。

避免空循环  在 C++ 和 Java 中，可以创建空循环，即循环所做的工作与检查工作是否完成测试写在同一行。以下是示例：

```
C++ Example of an Empty Loop
while ( ( inputChar = dataFile.GetChar() ) != CharType_Eof ) {
    ;
}
```

在此示例中，循环为空，因为 while 表达式包含两件事：循环的工作——inputChar = dataFile.GetChar()——以及循环是否应终止的测试——inputChar != CharType_Eof。如果重新编码循环，使其所做的工作对读者明显，循环会更清晰：

```
C++ Example of an Empty Loop Converted to an Occupied Loop
do {
    inputChar = dataFile.GetChar();
} while ( inputChar != CharType_Eof );
```

新代码占用三行而不是一行和一个分号，这是合适的，因为它做了三行工作而不是一行和一个分号的工作。

## 将循环维护工作保持在循环的开头或结尾

循环维护工作是像 i = i + 1 或 j++ 这样的表达式，其主要目的不是做循环的工作而是控制循环。在此示例中，维护工作在循环末尾完成：

```
C++ Example of Housekeeping Statements at the End of a Loop
nameCount = 0;
totalLength = 0;
while ( !inputFile.EndOfFile() ) {
    // do the work of the loop
    inputFile >> inputString;
    names[ nameCount ] = inputString;
    ...
    // prepare for next pass through the loop--housekeeping
    nameCount++;
    totalLength = totalLength + inputString.length();
}
```

以下是维护语句。

作为一般规则，你在循环前初始化的变量就是你在循环的维护部分中操作的变量。

## 使每个循环只执行一个功能

仅仅因为一个循环可以同时做两件事，并不足以证明将它们放在一起的理由。循环应像例程一样，每个循环只做一件事并且做好它。如果使用两个循环而不是一个循环似乎效率低下，就将代码写成两个循环，注释说明它们可以为了效率而合并，然后等待基准测试显示程序的该部分存在性能问题后再将两个循环改为一个。

> Cross-Reference For more on optimization, see Chapter 25, "Code-Tuning Strategies," and Chapter 26, "Code-Tuning Techniques."

