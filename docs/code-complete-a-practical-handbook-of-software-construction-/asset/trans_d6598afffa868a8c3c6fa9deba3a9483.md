

C 或 C++ 或另一种语言中的等价物。下面是在 C++ 中设置类型定义的方法：

```
**C++ Example of Creating a Type**
```cpp
typedef float Coordinate;  // for coordinate variables
```
```

此类型定义声明了一个新的类型 *Coordinate*，其功能上与类型 float 相同。要使用新类型，你可以像使用预定义类型 *float* 一样声明变量。下面是一个示例：

```
**C++ Example of Using the Type You’ve Created**
```cpp
Routine1( ... ) {
    Coordinate latitude;     // latitude in degrees
    Coordinate longitude;    // longitude in degrees
    Coordinate elevation;    // elevation in meters from earth center
    ...
}
...

Routine2( ... ) {
    Coordinate x;    // x coordinate in meters
    Coordinate y;    // y coordinate in meters
    Coordinate z;    // z coordinate in meters
    ...
}
```
```

在此代码中，变量 *latitude*、*longitude*、*elevation*、*x*、*y* 和 *z* 都被声明为 *Coordinate* 类型。

现在假设程序发生了变化，你发现最终还是需要使用双精度变量来表示坐标。由于你专门为坐标数据定义了一个类型，你所要做的只是更改类型定义。而且你只需要在一个地方更改它：在 *typedef* 语句中。下面是更改后的类型定义：

```
**C++ Example of Changed Type Definition**
```cpp
typedef double Coordinate;  // for coordinate variables
```
```

![](img/649c8eee28c38ca1e062691e45dc9883_348_0.png)

下面是第二个示例——这次是 Pascal。假设你正在创建一个工资系统，其中员工姓名最长为 30 个字符。你的用户告诉你，没有人的名字会超过 30 个字符。你会在整个程序中硬编码数字 30 吗？如果你这样做，你对用户的信任就比我对我的用户的信任要高得多！更好的做法是为员工姓名定义一个类型：

```
**Pascal Example of Creating a Type for Employee Names**
```pascal
Type
    employeeName = array[ 1..30 ] of char;
```
```

当涉及字符串或数组时，通常明智的做法是定义一个命名常量来表示字符串或数组的长度，然后在类型定义中使用该命名常量。你会在程序的许多地方使用该常量——这只是你使用它的第一个地方。下面是它的样子：

### Pascal Example of Better Type Creation

```
Const
  NAME_LENGTH = 30;
  ...
Type
  employeeName = array[ 1..NAME_LENGTH ] of char;
```

这里是命名常量的声明。

这里是命名常量的使用位置。

更强大的示例将创建自己的类型与信息隐藏的思想结合起来。在某些情况下，你想要隐藏的信息是关于数据类型的信息。

C++ 中的坐标示例在信息隐藏方面已经走了一半。如果你始终使用 Coordinate 而不是 float 或 double，你就有效地隐藏了数据的类型。在 C++ 中，这就是语言为你提供的全部信息隐藏能力。对于其余部分，你或你代码的后续使用者必须有纪律地不去查找 Coordinate 的定义。C++ 给你的是比喻上的，而不是字面上的信息隐藏能力。

其他语言，如 Ada，则更进一步，支持字面上的信息隐藏。下面是 Coordinate 代码片段在声明它的 Ada 包中会是什么样子：

### Ada Example of Hiding Details of a Type Inside a Package

```
package Transformation is
  type Coordinate is private;
  ...
```

此语句将 Coordinate 声明为包的私有类型。

下面是 Coordinate 在另一个使用它的包中的样子：

### Ada Example of Using a Type from Another Package

```
with Transformation;
...
procedure Routine1(...) ...
  latitude: Coordinate;
  longitude: Coordinate;
begin
  -- statements using latitude and longitude
...
end Routine1;
```

请注意，*Coordinate* 类型在包规范中被声明为 *private*。这意味着程序中唯一知道 *Coordinate* 类型定义的部分是 *Transformation* 包的私有部分。在一个由一组程序员组成的开发环境中，你可以只分发包规范，这会使在另一个包上工作的程序员更难查找 *Coordinate* 的底层类型。信息将被字面地隐藏。像 C++ 这样要求你在头文件中分发 *Coordinate* 定义的语言会破坏真正的信息隐藏。

这些示例说明了创建自己的类型的几个原因：

- **To make modifications easier**  创建新类型的工作量很小，但能给你很大的灵活性。
- **To avoid excessive information distribution**  硬编码类型会将数据类型细节分散到程序各处，而不是集中在一个地方。这是第 6.2 节中讨论的信息隐藏原则集中化的一个例子。
- **To increase reliability**  在 Ada 中，你可以定义诸如 *type Age is range 0..99* 之类的类型。编译器随后会生成运行时检查，以验证任何 Age 类型的变量始终在 0..99 范围内。
- **To make up for language weaknesses**  如果你的语言没有你想要的预定义类型，你可以自己创建它。例如，C 没有布尔或逻辑类型。这种缺陷很容易通过自己创建类型来弥补：
  
  ```c
  typedef int Boolean;
  ```

### Why Are the Examples of Creating Your Own Types in Pascal and Ada?

Pascal 和 Ada 已经走上了剑龙的道路，并且通常取代它们的语言更易用。然而，在简单类型定义方面，我认为 C++、Java 和 Visual Basic 代表了三步前进、一步后退的情况。像

```
currentTemperature: INTEGER range 0..212;
```

这样的 Ada 声明包含重要的语义信息，而像

```
int temperature;
```

这样的语句则没有。再进一步，类型声明

```
type Temperature is range 0..212;
...
currentTemperature: Temperature;
```

允许编译器确保 *currentTemperature* 仅分配给具有 *Temperature* 类型的其他变量，并且提供这种额外安全边际所需的额外编码非常少。

当然，程序员可以创建一个 *Temperature* 类来强制执行 Ada 语言自动强制执行的相同语义，但从一行代码创建简单数据类型到创建类的步骤是一个很大的跨越。在许多情况下，程序员会创建简单类型，但不会付出额外努力去创建类。

### Guidelines for Creating Your Own Types

> **Cross-Reference** 在每种情况下，考虑是否创建类可能比简单数据类型更好。详情请参阅第 6 章“Working Classes。”

在创建自己的“用户定义”类型时，请牢记以下准则：

***Create types with functionally oriented names***  避免类型名称引用类型底层计算机数据的种类。使用引用新类型所代表的现实世界问题部分的类型的名称。在之前的示例中，定义创建了坐标和名称的良好命名类型——现实世界的实体。同样，你可以为货币、付款代码、年龄等创建类型——现实世界问题的方面。

要警惕创建引用预定义类型的类型名称。像 *BigInteger* 或 *LongString* 这样的类型名称引用计算机数据而不是现实世界问题。创建自己的类型的主要优势在于它在你的程序和实现语言之间提供了一层绝缘。引用底层编程语言类型的类型名称会在该绝缘层上打孔。它们与使用预定义类型相比没有多大优势。而面向问题的名称则为你带来易于修改和自文档化的数据声明。

***Avoid predefined types***  如果类型可能发生变化，请避免在 *typedef* 或类型定义之外使用预定义类型。创建面向功能的新的类型很容易，而在程序中使用硬连线类型更改数据则很困难。此外，使用面向功能的类型的声明部分地记录了用它们声明的变量。像 *Coordinate x* 这样的声明比像 *float x* 这样的声明告诉你更多关于 x 的信息。尽可能多地使用自己的类型。

***Don’t redefine a predefined type***  更改标准类型的定义会造成混淆。例如，如果你的语言有一个预定义类型 *Integer*，不要创建自己的类型也叫 *Integer*。阅读你代码的人可能会忘记你重新定义了该类型，并假设他们看到的 *Integer* 是他们习惯看到的 *Integer*。

***Define substitute types for portability***  与你不应该更改标准类型定义的建议相反，你可能希望为标准类型定义替代类型，以便在不同的硬件平台上使变量表示完全相同的实体。例如，你可以定义一个类型 *INT32* 并使用它

