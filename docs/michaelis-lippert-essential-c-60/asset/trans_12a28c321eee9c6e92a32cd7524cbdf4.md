
Well-formed types
  判断两个对象是否相等，392-395
  实现 Equals() 等价运算符，392-395
  延迟初始化，429-431
  对象标识 vs. 相等对象值，388-392
  重写 Equals() 等价运算符，392-395
Well-formed types, garbage collection. See also Resource cleanup.
  Collect() 方法，419
  介绍，418
  在 .NET 中，418-419
  根引用，418
  强引用，420-421
  弱引用，420-421
Well-formed types, namespaces
  在 CLR（Common Language Runtime）中，410
  extern alias 指令，413
  指南，412
  介绍，409-410
  命名空间别名限定符，412-413
  命名约定，410
  嵌套，411
Well-formed types, overloading object members
  Equals() 等价运算符，388-395
  GetHashCode() 方法，385-387
  ToString() 方法，384-385
Well-formed types, overloading operators
  二元运算符，397-399
  与赋值运算符结合的二元运算符，397-399
  强制转换运算符，402
  条件逻辑运算符，400
  转换运算符，401, 403
  一元运算符，400-401
Well-formed types, referencing other assemblies
  更改程序集目标，404
  类库，404-405
  控制台可执行文件，404
  类型的封装，407-408
  类型声明上的 internal 访问修饰符，407-408
  模块，405
  PCLs（便携类库），406
protected internal 类型修饰符，408
public 访问修饰符 on type declarations，407-408
referencing assemblies，405-406
referencing assemblies on Mac and Linux，406
type member accessibility modifiers，409. See also specific modifiers.
Windows executables，405
Well-formed types, resource cleanup
  从构造函数传播异常，428
  析构，421-427
  析构队列，426
  垃圾回收，426-427
  指南，428
  使用 IDisposable，424-425, 426-427
  介绍，421
  调用 using 语句，425-426
  复活对象，429
Well-formed types, XML comments
  与编程构造关联，414-416
  生成 XML 文档文件，416-418
  指南，418
  介绍，413-414
when clauses, catching exceptions，438
where clauses，623-624, 631-632
Where() 方法，591-592, 597-598
while loops，108, 134-135, 136-137
while() 方法，584
while statement，108, 134-135, 136-137
Whitespace，12, 13
Win32, error handling in P/Invoke，855-857
Windows Desktop CLR compiler，880
Windows Runtime. See WinRT.
WinRT. See also P/Invoke.
  自动 shim 接口，875-876
  定义，896
  描述，873-874
  基于任务的异步，876
WinRT events，874-875
Work stealing，802-803
Wrappers for API calls from P/Invoke，860-861
Write() 方法
  开始新行，48, 55
  写入控制台，19-21
WriteLine() 方法
  往返格式化，44-45
  开始新行，48, 55
  写入控制台，19-21
Write-only properties，247-248
WriteWebRequestSizeAsync() 方法，780, 783
guidelines，418
introduction，413-414
single-line，24

## X

XML (Extensible Markup Language)，25, 416-418
XML comments
  与编程构造关联，414-416
  限定注释，24
  生成 XML 文档文件，416-418

## Y

yield break statement，677-678
yield keyword，6
yield return statement
  在 foreach 循环中，674-676
  实现 BinaryTree<T>，673-676
  要求，681
  返回迭代器值，670-671
yield return statements，6

## Z

ZipCompression，337

## Index of 6.0 Topics

Operators
?. (question mark, dot), null-conditional operator，125–128
. (dot) dot operator，126

A
ArgumentNullException，434-435, 436
ArgumentOutOfRangeException，435, 436
Arrays, initializing anonymous type，579-580
Automatically implemented properties initializing，242
NextId implementation，273
read-only，248, 280

B
Boolean expressions, logical operators
?. (question mark, dot), null-conditional operator，125–128
. (dot) dot operator，126

C
Catching exceptions. See also Exception handling; Throwing exceptions.
conditional clauses，438
exception conditions，438
rethrowing existing exceptions，438-439
System.InvalidOperationException，438
when clauses，438
Classes, inextensible，273-275
Collection initializers, initializing anonymous type arrays，579-580
Conditional clauses, catching exceptions，438

D
default operator，360-361
Delegates, with the null-conditional operator，128

E
Exception handling. See also Catching exceptions; Throwing exceptions. guidelines，445
passing null exceptions，434

I
Immutability of value types，357
Invoke() 方法，548-549

M
Methods, declaring
example，169-170
expression bodied methods，174
Move() 方法，357

N
nameof operator，246-247, 435, 436, 694-696
Namespaces, dropping，53-54. See also using directive.
.NET versions，29
new operator，359-360
NextId implementation，273
NextId initialization，273
null, checking code for，548
NullReferenceException，128, 434, 436

O
OutOfMemoryException，435

## P

Properties
  automatically implemented，242, 248, 273, 280
  nameof operator，246-247
  read-only，248, 280
Publishing code, checking for null，548

## R

readonly modifier，280
Read-only properties，248, 280

## S

struct keyword，356
Structs
  declaring，356
  default value for，360-361
  definition，356
  finalizer support，360
  initializing，357-359
  referential identity，360
System.ApplicationException，435, 436
System.ArgumentException，436
System.Environment.FailFast() 方法，435, 436
System.Exception，435, 436
System.ExecutionEngineException，435
System.InvalidOperationException，438
System.OutOfMemoryException，435
System.Runtime.InteropServices.COMException，435
System.Runtime.InteropServices.SEHException，435
System.StackOverflowException，435
System.SystemException，435, 436

## T

TextNumberParser.Parse() 方法，434
Throwing exceptions
  ArgumentNullException，434-435, 436
  ArgumentOutOfRangeException，435, 436
  code sample，434
  identifying the parameter name，435
  nameof operator，435, 436
  NullReferenceException，434, 436
  rethrowing，438-439
  System.ApplicationException，435, 436
  System.ArgumentException，436
  System.Environment.FailFast() 方法，435, 436
  System.Exception，435, 436
  System.ExecutionEngineException，435
  System.OutOfMemoryException，435
  System.Runtime.InteropServices.COMException，435
  System.Runtime.InteropServices.SEHException，435
  System.StackOverflowException，435
  System.SystemException，435, 436
Type names, abbreviating，178-179

## U

using directive
  dropping namespaces，53-54
  example，53-54
using static directive
  abbreviating a type name，178-179
  dropping namespaces，53-54
  example，53-54, 178-179

## V

Value types
  default operator，360-361
  immutability，357
  new operator，359-360

## W

when clauses，438

## Index of 5.0 Topics

Operators
.... (periods), download progress indicator，779

A
AggregateException，762-765
AggregateException.Flatten() 方法，780
AggregateException.Handle() 方法，764, 780
Anonymous functions, guidelines，533
Antecedent tasks，757
AspNetSynchronizationContext，794
async keyword
  purpose of，786
  task-based asynchronous pattern，781-786, 795-798
Asynchronous
  continuations，756-762
  high-latency operations with the TPL，777-781
  lambdas，786-787
  tasks. See Multithreading, asynchronous tasks.
AttachedToParent enum，758
await keyword, task-based asynchronous pattern，781-786, 791-792, 795-798
await operators, task-based asynchronous pattern，797-798

B
Break() 方法，808
Breaking parallel loop iterations，808

C
Canceling
  cooperative cancellation，769
  multithreading, PLINQ queries，811-813
  parallel loop iterations，805-806
  tasks. See Multithreading, canceling tasks.
CancellationToken object，769-772
CancellationTokenSource.Cancel() 方法，770-771
Capturing loop variables with lambda expressions，531-533
Chaining tasks，757
Composing large tasks from smaller one，756-758
Continuation tasks，757
ContinueWith() 方法，756-758, 760-761, 764 765, 779
Control flow
  misconceptions，784
  multithreading asynchronous tasks，755
  within tasks，784-786
Cooperative cancellation, definition，769
CountdownEvent，840
Custom asynchronous methods，787-791

D
DenyChildAttach enum，758
DispatcherSynchronizationContext，794
Disposable tasks，774

E
Exception handling
  parallel loop iterations，803-804

