

## 注释数据声明

交叉引用 有关格式化数据的详细信息，请参阅第 31.5 节中的“布置数据声明”。有关如何有效使用数据的详细信息，请参阅第 10 章至第 13 章。

变量声明的注释描述的是变量名无法描述的变量方面。仔细记录数据非常重要；至少有一家研究了自身实践的公司得出了结论，数据上的注释甚至比数据所使用过程中的注释更重要（SDC，载于 Glass 1982）。以下是注释数据的一些指导原则：

**注释数值数据的单位** 如果一个数字代表长度，请说明该长度是以英寸、英尺、米还是公里表示的。如果是时间，请说明它是自 1980-1-1 以来的经过秒数、程序开始以来的毫秒数等等。如果是坐标，请说明它们是否代表纬度、经度、高度以及它们是以弧度还是度表示；是否代表以地球中心为原点的 X、Y、Z 坐标系等等。不要假设单位是显而易见的。对新程序员来说，它们不会。对正在处理系统另一部分的人来说，它们不会。在程序经过大幅修改后，它们也不会。

或者，在许多情况下，您应该将单位嵌入变量名中而不是放在注释中。像 *distanceToSurface = marsLanderAltitude* 这样的表达式看起来可能是正确的，但 *distanceToSurfaceInMeters = marsLanderAltitudeInFeet* 则暴露了明显的错误。

交叉引用 记录变量允许范围的更强技术是在例程的开头和结尾使用断言，以断言变量的值应在规定的范围内。有关详细信息，请参阅第 8.2 节“断言”。

**注释允许的数值范围** 如果变量有预期的值范围，请记录预期范围。Ada 编程语言的强大功能之一是能够将数值变量的允许值限制在一定范围内。如果您的语言不支持该功能（大多数语言都不支持），请使用注释来记录预期值范围。例如，如果变量代表美元金额，请说明您期望它在 $1 到 $100 之间。如果变量表示电压，请说明它应介于 105v 和 125v 之间。

**注释编码含义** 如果您的语言支持枚举类型——如 C++ 和 Visual Basic——请使用它们来表达编码含义。如果不支持，请使用注释说明每个值代表什么——并为每个值使用命名常量而不是字面量。如果变量代表电流种类，请注释 1 代表交流电，2 代表直流电，3 代表未定义。

以下是说明变量声明的示例，说明了前面三个建议——所有范围信息都以注释形式给出：

**Visual Basic 示例：注释良好的变量声明**

```vb
Dim cursorX As Integer   ' horizontal cursor position; ranges from 1..MaxCols
Dim cursorY As Integer   ' vertical cursor position; ranges from 1..MaxRows

Dim antennaLength As Long      ' length of antenna in meters; range is >= 2
Dim signalStrength As Integer  ' strength of signal in kilowatts; range is >= 1

Dim characterCode As Integer     ' ASCII character code; ranges from 0..255
Dim characterAttribute As Integer ' 0=Plain; 1=Italic; 2=Bold; 3=Bold+Italic
Dim characterSize As Integer      ' size of character in points; ranges from 4..127
```

**注释输入数据的限制** 输入数据可能来自输入参数、文件或直接用户输入。前面的指导原则同样适用于例程输入参数和其他类型的数据。确保预期值和非预期值都已记录。注释是记录例程绝不应该接收某些数据的一种方式。断言是记录有效范围的另一种方式，如果您使用它们，代码就会变得更加自检。

**逐位记录标志** 如果变量用作位域，请记录每一位的含义：

> **交叉引用** 有关命名标志变量的详细信息，请参阅第 11.2 节中的“命名状态变量”。

**Visual Basic 示例：逐位记录标志**

```vb
• The meanings of the bits in statusFlags are as follows, from most
  significant bit to least significant bit:
• MSB    0       error detected: 1=yes, 0=no
         1–2     kind of error: 0=syntax, 1=warning, 2=severe, 3=fatal
         3       reserved (should be 0)
         4       printer status: 1=ready, 0=not ready
         ...
         14      not used (should be 0)
• LSB    15–32   not used (should be 0)
Dim statusFlags As Integer
```

如果该示例用 C++ 编写，它将需要位域语法，以便位域含义能够自文档化。

**用变量名标记与变量相关的注释** 如果您有引用特定变量的注释，请确保在变量更新时注释也会更新。提高一致修改几率的一种方法是使用变量名标记注释。这样，对变量名的字符串搜索也会找到注释以及变量本身。

> **交叉引用** 有关使用全局数据的详细信息，请参阅第 13.3 节“全局数据”。

**记录全局数据** 如果使用全局数据，请在声明点对每个数据项进行良好注释。注释应说明数据的用途以及为什么需要它是全局的。在每次使用数据的地方，都要明确该数据是全局的。命名约定是突出变量全局状态的首选方法。如果不使用命名约定，注释可以填补空白。

未嵌套的循环。当嵌套很深或循环很长时，这种技术就会发挥作用。

*将循环结束注释视为复杂代码的警告* 如果循环复杂到需要循环结束注释，请将该注释视为警告标志：循环可能需要简化。同样复杂的 if 测试和 case 语句也适用此规则。

循环结束注释提供了对逻辑结构的实用线索，但最初编写然后维护它们可能会变得繁琐。避免这种繁琐工作的最好方法通常是重写任何复杂到需要繁琐文档的代码。

## 注释例程

交叉引用 有关格式化例程的详细信息，请参阅第 31.7 节。有关如何创建高质量例程的详细信息，请参阅第 7 章。

![](img/649c8eee28c38ca1e062691e45dc9883_841_0.png)

例程级注释是典型计算机科学教科书中最糟糕建议的主题之一。许多教科书敦促您在每个例程顶部堆积一堆信息，无论其大小或复杂程度如何：

Visual Basic 示例：单体、万能的例程前言

```text
********************************************************************************
* Name: CopyString
*
* Purpose:     This routine copies a string from the source
               string (source) to the target string (target).
*
* Algorithm:   It gets the length of "source" and then copies each
               character, one at a time, into "target". It uses
               the loop index as an array index into both "source"
               and "target" and increments the loop/array index
               after each character is copied.
*
* Inputs:      input    The string to be copied
*
* Outputs:     output   The string to receive the copy of "input"
*
* Interface Assumptions: None
*
* Modification History: None
*
* Author:      Dwight K. Coder
* Date Created: 10/1/04
* Phone:       (555) 222-2255
* SSN:         111-22-3333
* Eye Color:   Green
* Maiden Name: None
* Blood Type:  AB-
* Mother's Maiden Name: None
* Favorite Car: Pontiac Aztek
* Personalized License Plate: "Tek-ie"
********************************************************************************
```

