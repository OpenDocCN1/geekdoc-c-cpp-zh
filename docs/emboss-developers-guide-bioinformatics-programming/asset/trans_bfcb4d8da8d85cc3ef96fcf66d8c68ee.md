

## D.6 函数文档

静态函数的结构化注释以 @funcstatic 开头，而导出函数则标记为 @func。对于导出函数，原型在相关头文件中声明。每个函数前的结构化注释必须采用以下一般格式：

```
/* @func FunctionName ***********************************************************
**
** FunctionDescription
** FunctionDescription cont.
**
** @param [ParameterCode1] ParameterName1 [Datatype1] Description
** @param [ParameterCode2] ParameterName2 [Datatype2] Description
** @return [Datatype] Description
** @cre Description
** @ure Description
** @exception ExceptName Description
** @see RelatedFunctionName
** @@
**
** Comments
** Comments cont.
***********************************************************************************/
Datatype FunctionName (Datatype ParameterName1, Datatype ParameterName2)
{
    /* Function C code goes here */
}
```

其中：

- FunctionName 是函数的名称。
- FunctionDescription 是出现在在线文档中的函数描述。它可以跨多行。
- ParameterCode* 是描述参数的参数代码（见下文），后跟对参数的简短描述。
- Datatype 是参数的数据类型或函数返回的数据类型（对于 void 函数则为 void）。
- RelatedFunctionName 是与所讨论函数相关的函数的名称。
- Comments 是可选注释，不会出现在在线文档中。

例如：

```
/* @func ajStrMatchC *************************************************************
**
** Simple test for matching a string and a text string.
**
** @param [r] str [const AjPStr] String
** @param [r] txt2 [const char*] Text
** @return [AjBool] ajTrue if two complete strings are the same
** @@
********************************************************************************/
AjBool ajStrMatchC(const AjPStr str, const char* txt2)
{
    if(!str || !txt2)
        return ajFalse;

    if(!strcmp(str->Ptr, txt2))
        return ajTrue;

    return ajFalse;
}
```

### D.6.1 函数文档标签

可用标签以 @ 开头，并基于 JavaDoc 中定义的集合。

| Tag | Description |
| :--- | :--- |
| @func | 结构化注释的开始，后跟函数名称和任意数量的带标记的自由文本行。如果函数不公开可见，请使用 @funcstatic。 |
| @funcstatic | 与 @func 相同，但用于静态（内部）函数。 |
| @param | 每个参数使用一次。参数名称（ParameterName）和类型（Datatype）与函数中定义的相同。还给出了参数代码（ParameterCode）（见下文）。 |
| @cre | 参数的已检查运行时错误的描述。 |
| @ure | 参数的未检查运行时错误的描述。 |
| @return | 成功执行时返回值的数据类型和描述。 |
| @error | 错误条件下返回值的描述。如果合适，可以使用多次。 |
| @exception | 此函数抛出的异常。如果合适，可以使用多次。 |
| @see | 相关函数的交叉引用。必须给出一个函数名称（RelatedFunctionName），它与同一或不同源文件中 @func 标签后给出的名称相同。 |
| @@ | 有效地结束结构化注释。任何后续文本都会被 HTML 转换解析器忽略，不会出现在在线文档中。 |

### D.6.2 参数代码

代码由基本类型的小写字母和大写修饰符组成。

| Code | Mnemonic | Description |
|---|---|---|
| *参数代码（基本类型）* | | |
| r | 读取 | 参数值被使用但不会以任何方式更改。 |
| w | 写入 | 参数值被忽略。除非满足特定条件（应予以文档化），否则始终会写入新值。 |
| u | 更新 | 参数值被使用，并且（通常）会写入新值。 |
| d | 删除 | 参数值是指向要释放的内存的指针。指针将被设置为 NULL。 |
| f | 函数指针 | 参数值是指向函数的指针。描述应指示函数类型。 |
| v | 可变参数 | 参数值是某种形式的可变长度参数列表。 |
| *参数代码（修饰符）* | | |
| C | 已检查 | 值会被检查。有关已检查的运行时错误，请参见 @cre 标签。 |
| E | 空 | 将接受空值，例如长度为零的字符串。 |
| N | 空 | 将接受 NULL 值。 |
| P | 指针 | 如果指针本身可能被写入，而不仅仅是它指向的数据，请使用此项。 |

## 附录 E 资源

### E.1 EMBOSS 编程接口

下面描述了 EMBOSS 的编程接口。

> **注意**
> 接口列表绝非详尽无遗。如果您了解其他与 EMBOSS 相关的接口，请将详细信息发送至 emboss-bug@emboss.open-bio.org。

可用的编程接口包括：

| Interface | Link | Description |
|---|---|---|
| Biopython | http://www.biopython.org | 各种模块使用 EMBOSS 程序。 |
| Bio-Emboss | http://search.cpan.org/dist/Bio-Emboss/ | 一个 Perl 接口，用于 EMBOSS 库，允许您编写看起来和感觉像典型 EMBOSS 程序的 Perl 程序。 |
| BioPerl 类用于 EMBOSS 应用程序 Bio::Tools::Run::EMBOSS Application | http://doc.bioperl.org/releases/bioperl-1.0.2/Bio/Tools/Run/EMBOSSApplication.html | EMBOSSApplication 类可以表示任何 EMBOSS 应用程序。它由 Bio::Factory::EMBOSS 对象创建，该对象通过读取应用程序 ADC 文件对其进行初始化。 |
| BioPerl EMBOSS 应用程序工厂类 Bio::Factory::EMBOSS | http://doc.bioperl.org/bioperl-run/Bio/Factory/EMBOSS.html | EMBOSS 工厂类封装了对现有 EMBOSS 程序的访问。 |
| BioPerl 类用于 EMBOSS 应用程序限定符 Bio::Tools::Run::EMBOSSacd | http://search.cpan.org/~birney/bioperl-run-1.4/Bio/Tools/Run/EMBOSSacd.pm | EMBOSSacd 类表示可以传递给 EMBOSS 应用程序的所有可能命令行参数。 |
| BioMoby | http://biomoby.open-bio.org/ | MOBY 是一个本体学系统，用于生物服务提供商（无论是数据主机还是分析服务）之间的互操作性。EMBOSS 应用程序已被纳入。 |

### SOAPLAB

http://www.ebi.ac.uk/Tools/webservices/soaplab/overview

**SoapLab** 为命令行程序生成 Web 服务。可能有两种 Web 服务接口（通用接口和类型化接口）。通用接口允许将输入数据作为弱类型名称:值对发送。这允许将各种应用程序集成在单个编程接口下。类型化 Web 服务接口在 WSDL/XSD 级别定义输入/输出类型描述，允许 Web 服务客户端使用标准方法检查输入/输出数据类型。

## 索引

### 符号

-debug 选项（参见 调试）
./configure 命令（参见 配置脚本）
.embossrc 文件（参见 EMBOSS 配置文件）
ACD 应用程序属性，91, 92, 485, 513
ACD 应用程序定义，25, 61, 83, 91, 425, 434, 459, 484, 485
属性（参见 ACD 应用程序属性）
检索某个的值（参见 操作）
ACD 属性，81, 436, 484, 489
应用程序（参见 ACD 应用程序属性）
计算的（参见 计算属性）
数据（参见 ACD 数据属性）
全局的（参见 全局属性）
ACD 计算，123, 140
类型，564
变量和，127, 566
ACD 数据属性，83, 96, 486, 525, 556
计算的（参见 计算属性）
特定于数据类型的，109（参见 特定于数据类型的属性）
用于与数据类型关联的限定符，114
用于定义数据输出，113, 522
用于定义帮助信息，108, 523
用于定义最大值和最小值，96, 132
用于图形 ACD 数据类型，114, 555
用于输入 ACD 数据类型，110, 530, 557
用于命名和定位文件，111, 112
用于输出 ACD 数据类型，111, 540
用于选择 ACD 数据类型，113, 554
用于设置默认值，96, 131
用于简单 ACD 数据类型，525, 557
用于类型检查输入，110, 111, 522
用于用户提示，105, 129, 133, 521
用于验证应用程序输出，113
用于验证用户输入，107, 110, 523
全局的（参见 全局属性）
检索值（参见 操作）
类型，103, 489
ACD 数据定义，96, 435, 485, 486
属性（参见 ACD 数据属性）
检索某个的值（参见 操作）
ACD 数据类型，51, 98, 492
图形（参见 图形 ACD 数据类型）
输入（参见 输入 ACD 数据类型）
输出（参见 输出 ACD 数据类型）
选择（参见 选择 ACD 数据类型）
简单（参见 简单 ACD 数据类型）

ACD 定义
用于应用程序定义（参见 ACD 应用程序定义）
用于数据定义（参见 ACD 数据定义）
ACD 文件名（参见 ACD 文件）
ACD 文件节，96, 486, 490, 491
附加，491
高级，491
输出，491
所需，491
验证，491
ACD 文件节文件（参见 sections.standard 文件）
ACD 文件，19, 25, 34, 38, 61, 81, 433, 455
属性（参见 ACD 数据属性）
中的数据类型（参见 ACD 数据类型）
调试（参见 调试）
文档化，424, 425
处理，188
位置，30
命名，92, 485
中的操作（参见 操作）
处理，189, 439, 465, 471, 480
重新格式化，143
从中检索值（参见 ajAcdGet 函数）
中的节（参见 ACD 文件节）
语法（参见 ACD 语法）
测试，26, 46, 62, 139, 142, 143
用于的实用程序（参见 ACD 实用程序）
ACD 操作（参见 操作）
ACD 运算符，121, 563
使用的否定，133, 565
ACD 语法，19, 82, 139, 484
ACD 实用程序，26, 62, 82, 136, 425, 456
ACD 变量，122, 127, 566
自动，39, 128, 567
定义，128
acdvalid, 139
由其测试的功能，140
aclocal, 4
其他限定符（参见 命令行限定符）
ACD 文件中的其他节（参见 ACD 文件节）
高级限定符（参见 命令行限定符）
ACD 文件中的高级节（参见 ACD 文件节）
ajAcdGet 函数，34, 43, 50, 162, 165, 189, 192, 193, 437, 440, 465, 477, 569
AJAX, 186, 569
文档，13, 19, 185, 568
扩展，60, 63, 72, 73, 154
AJAX 命令定义（参见 ACD 语法）
AJAX 命令定义文件（参见 ACD 文件）
AJAX 数据类型（参见 对象）
ajax.h 文件，64, 75, 147, 577

