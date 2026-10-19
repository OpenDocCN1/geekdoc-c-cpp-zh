

(Shneiderman 1980)。然而，短名称会带来许多问题，一些谨慎的程序员会出于防御性编程的策略而完全避免使用它们。

## 对全局命名空间中的名称使用限定符

如果您有位于全局命名空间中的变量（命名常量、类名等），请考虑是否需要采用一种约定来划分全局命名空间并避免命名冲突。在 C++ 和 C# 中，您可以使用 namespace 关键字来划分全局命名空间。

**使用 namespace 关键字划分全局命名空间的 C++ 示例**

```cpp
namespace UserInterfaceSubsystem {
...
// lots of declarations
...
}

namespace DatabaseSubsystem {
...
// lots of declarations
...
}
```

如果您在 UserInterfaceSubsystem 和 DatabaseSubsystem 中都声明了一个 Employee 类，您可以通过编写 UserInterfaceSubsystem::Employee 或 DatabaseSubsystem::Employee 来标识您想要引用的类。在 Java 中，您可以通过使用包来实现同样的效果。

在不支持命名空间或包的语言中，您仍然可以使用命名约定来划分全局命名空间。一种约定是要求全局可见的类以子系统助记符为前缀。用户界面员工类可能变成 uiEmployee，而数据库员工类可能变成 dbEmployee。这最大限度地降低了全局命名空间冲突的风险。

## 变量名中的计算值限定符

许多程序都有包含计算值的变量：总数、平均值、最大值等。如果您用像 Total、Sum、Average、Max、Min、Record、String 或 Pointer 这样的限定符修改名称，请将修饰符放在名称的末尾。

这种做法有几个优点。首先，变量名称中最重要的部分，即赋予变量大部分含义的部分，位于前面，因此更突出且先被阅读。其次，通过建立这种约定，您可以避免可能产生的混淆，如果您在同一程序中使用 totalRevenue 和 revenueTotal。名称在语义上是等价的，而约定会防止它们被当作不同的名称使用。第三，像 revenueTotal、expenseTotal、revenueAverage 和 expenseAverage 这样的名称集合具有令人愉悦的对称性。而像 *totalRevenue*、*expenseTotal*、*revenueAverage* 和 *averageExpense* 这样的名称集合则不令人感到有序。最后，一致性提高了可读性并简化了维护。

计算值放在名称末尾规则的一个例外是 *Num* 限定符的惯用位置。放在变量名称开头时，*Num* 指的是总数：*numCustomers* 是客户总数。放在变量名称末尾时，*Num* 指的是索引：*customerNum* 是当前客户的编号。*numCustomers* 末尾的 *s* 也是意义差异的另一个提示。但是，由于使用 *Num* 经常会造成混淆，最好通过使用 *Count* 或 *Total* 来指代客户总数，使用 *Index* 来指代特定客户，从而完全避开这个问题。因此，*customerCount* 是客户总数，而 *customerIndex* 指的是特定客户。

## 变量名中的常见反义词

> **交叉引用** 有关例程名称中类似的反义词列表，请参阅第 7.3 节中的“精确使用反义词”。

精确使用反义词。使用反义词的命名约定有助于一致性，从而提高可读性。像 *begin/end* 这样的配对很容易理解和记忆。偏离常用语言反义词的配对往往难以记忆，因此令人困惑。以下是一些常见反义词：

- begin/end
- first/last
- locked/unlocked
- min/max
- next/previous
- old/new
- opened/closed
- visible/invisible
- source/target
- source/destination
- up/down

## 11.2 命名特定类型的数据

除了命名数据的一般考虑之外，在命名特定类型的数据时也会出现特殊考虑。本节描述了针对循环变量、状态变量、临时变量、布尔变量、枚举类型和命名常量的具体考虑。

### 命名循环索引

> **交叉引用** 有关循环的详细信息，请参阅第 16 章“控制循环”。

由于循环是计算机编程中常见的特性，因此出现了命名循环变量的指导方针。*i*、*j* 和 *k* 是惯用的名称：

**简单循环变量名称的 Java 示例**

```java
for ( i = firstItem; i < lastItem; i++ ) {
    data[ i ] = 0;
}
```

如果变量要在循环外部使用，则应赋予比 *i*、*j* 或 *k* 更有意义的名称。例如，如果您正在从文件中读取记录并且需要记住已读取的记录数，像 *recordCount* 这样的名称就很合适：

**良好描述性循环变量名称的 Java 示例**

```java
recordCount = 0;
while ( moreScores() ) {
    score[ recordCount ] = GetNextScore();
    recordCount++;
}

// lines using recordCount
```

如果循环超过几行，很容易忘记 *i* 代表什么，这时最好给循环索引一个更有意义的名称。由于代码经常被更改、扩展并复制到其他程序中，许多经验丰富的程序员完全避免使用像 *i* 这样的名称。

循环变长的一个常见原因是它们是嵌套的。如果您有多个嵌套循环，请为循环变量分配更长的名称以提高可读性。

**嵌套循环中良好循环名称的 Java 示例**

```java
for ( teamIndex = 0; teamIndex < teamCount; teamIndex++ ) {
    for ( eventIndex = 0; eventIndex < eventCount[ teamIndex ]; eventIndex++ ) {
        score[ teamIndex ][ eventIndex ] = 0;
    }
}
```

精心选择的循环索引变量名称避免了索引串扰的常见问题：说 *i* 时实际意思是 *j*，说 *j* 时实际意思是 *i*。它们还使数组访问更清晰：*score[ teamIndex ][ eventIndex ]* 比 *score[ i ][ j ]* 更具信息性。

如果您必须使用 *i*、*j* 和 *k*，不要将它们用于除简单循环的循环索引之外的任何用途——该约定已过于确立，打破它用于其他方式会令人困惑。避免此类问题的最简单方法是简单地为 *i*、*j* 和 *k* 思考出更有描述性的名称。

### 命名状态变量

状态变量描述程序的状态。以下是命名指导原则：

**为状态变量想一个比 flag 更好的名称** 最好将标志视为状态变量。标志的名称中永远不应包含 flag，因为这并不能让您了解标志的作用。为了清晰，标志应分配值，并且其值应使用枚举类型、命名常量或充当命名常量的全局变量进行测试。以下是一些名称不好的标志示例：

![](img/649c8eee28c38ca1e062691e45dc9883_302_0.png)

**晦涩标志的 C++ 示例**

```cpp
if ( flag ) ...
if ( statusFlag & 0x0F ) ...
if ( printFlag == 16 ) ...
if ( computeFlag == 0 ) ...

flag = 0x1;
statusFlag = 0x80;
printFlag = 16;
computeFlag = 0;
```

语句如 *statusFlag = 0x80* 除非您编写了代码或有文档说明 *statusFlag* 是什么以及 *0x80* 代表什么，否则不会让您了解代码的作用。以下是更清晰的等效代码示例：

**状态变量更好使用的 C++ 示例**

```cpp
if ( dataReady ) ...
if ( characterType & PRINTABLE_CHAR ) ...
if ( reportType == ReportType_Annual ) ...
if ( recalcNeeded == True ) ...

dataReady = true;
characterType = CONTROL_CHARACTER;
reportType = ReportType_Annual;
recalcNeeded = false;
```

显然，*characterType = CONTROL_CHARACTER* 比 *statusFlag = 0x80* 更有意义。同样，条件 *if ( reportType == ReportType_Annual )* 比 *if ( printFlag == 16 )* 更清晰。第二个示例表明您也可以使用枚举类型以及预定义命名常量来采用这种方法。以下是您如何使用命名常量和枚举类型来设置示例中使用的值：

**在 C++ 中声明状态变量**

```cpp
// values for CharacterType
const int LETTER = 0x01;
const int DIGIT = 0x02;
const int PUNCTUATION = 0x04;
const int LINE_DRAW = 0x08;
```
