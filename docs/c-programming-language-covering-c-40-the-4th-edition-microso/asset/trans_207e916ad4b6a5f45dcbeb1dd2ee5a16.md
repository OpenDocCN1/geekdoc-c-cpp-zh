
interface-member-declarations:
  interface-member-declaration
  interface-member-declarations interface-member-declaration

interface-member-declaration:
  interface-method-declaration
  interface-property-declaration
  interface-event-declaration
  interface-indexer-declaration

interface-method-declaration:
  attributes_opt new_opt return-type identifier type-parameter-list
  ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

interface-property-declaration:
  attributes_opt new_opt type identifier { interface-accessors }

interface-accessors:
  attributes_opt get ;
  attributes_opt set ;
  attributes_opt get ; attributes_opt set ;
  attributes_opt set ; attributes_opt get ;

interface-event-declaration:
  attributes_opt new_opt event type identifier ;

interface-indexer-declaration:
  attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }

## B.2.11 枚举

```
enum-declaration:
  attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
  : integral-type

enum-body:
  { enum-member-declarations_opt }
  { enum-member-declarations , }

enum-modifiers:
  enum-modifier
  enum-modifiers enum-modifier
```

## B.2.12 委托

## B.2.13 属性

```
enum-modifier:
  new
  public
  protected
  internal
  private

enum-member-declarations:
  enum-member-declaration
  enum-member-declarations , enum-member-declaration

enum-member-declaration:
  attributes_opt identifier
  attributes_opt identifier = constant-expression

delegate-declaration:
  attributes_opt delegate-modifiers_opt delegate return-type
  identifier variant-type-parameter-list
  ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

delegate-modifiers:
  delegate-modifier
  delegate-modifiers delegate-modifier

delegate-modifier:
  new
  public
  protected
  internal
  private

global-attributes:
  global-attribute-sections

global-attribute-sections:
  global-attribute-section
  global-attribute-sections global-attribute-section

global-attribute-section:
  [ global-attribute-target-specifier attribute-list ]
  [ global-attribute-target-specifier attribute-list , ]
```

## B. 语法

```
global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    assembly
    module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections attribute-section

attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]

attribute-target-specifier:
    attribute-target :

attribute-target:
    field
    event
    method
    param
    property
    return
    type

attribute-list:
    attribute
    attribute-list , attribute

attribute:
    attribute-name attribute-arguments_opt

attribute-name:
    type-name

attribute-arguments:
    ( positional-argument-list_opt )
    ( positional-argument-list , named-argument-list )
    ( named-argument-list )
```

```
positional-argument-list:
    positional-argument
    positional-argument-list  ,  positional-argument
```

```
positional-argument:
    argument-name<sub>opt</sub>  attribute-argument-expression
```

```
named-argument-list:
    named-argument
    named-argument-list  ,  named-argument
```

```
named-argument:
    identifier  =  attribute-argument-expression
```

```
attribute-argument-expression:
    expression
```

## B.3 不安全代码的语法扩展

```
class-modifier:
    ...
    unsafe
```

```
struct-modifier:
    ...
    unsafe
```

```
interface-modifier:
    ...
    unsafe
```

```
delegate-modifier:
    ...
    unsafe
```

```
field-modifier:
    ...
    unsafe
```

```
method-modifier:
    ...
    unsafe
```

```
property-modifier:
  ...
  unsafe

event-modifier:
  ...
  unsafe

indexer-modifier:
  ...
  unsafe

operator-modifier:
  ...
  unsafe

constructor-modifier:
  ...
  unsafe

destructor-declaration:
  attributes_opt extern_opt unsafe_opt ~ identifier ( ) destructor-body
  attributes_opt unsafe_opt extern_opt ~ identifier ( ) destructor-body

static-constructor-modifiers:
  extern_opt unsafe_opt static
  unsafe_opt extern_opt static
  extern_opt static unsafe_opt
  unsafe_opt static extern_opt
  static extern_opt unsafe_opt
  static unsafe_opt extern_opt

embedded-statement:
  ...
  unsafe-statement
  fixed-statement

unsafe-statement:
  unsafe block

type:
  ...
  pointer-type
```

```
pointer-type:
    unmanaged-type *
    void *

unmanaged-type:
    type

primary-no-array-creation-expression:
    ...
    pointer-member-access
    pointer-element-access
    sizeof-expression

unary-expression:
    ...
    pointer-indirection-expression
    addressof-expression

pointer-indirection-expression:
    * unary-expression

pointer-member-access:
    primary-expression -> identifier type-argument-list_opt

pointer-element-access:
    primary-no-array-creation-expression [ expression ]

addressof-expression:
    & unary-expression

sizeof-expression:
    sizeof ( unmanaged-type )

fixed-statement:
    fixed ( pointer-type fixed-pointer-declarators ) embedded-statement

fixed-pointer-declarators:
    fixed-pointer-declarator
    fixed-pointer-declarators , fixed-pointer-declarator

fixed-pointer-declarator:
    identifier = fixed-pointer-initializer
```

fixed-pointer-initializer:
  & variable-reference
  expression

struct-member-declaration:
  ...
  fixed-size-buffer-declaration

fixed-size-buffer-declaration:
  attributes_opt fixed-size-buffer-modifiers_opt fixed buffer-element-type
  fixed-size-buffer-declarators ;

fixed-size-buffer-modifiers:
  fixed-size-buffer-modifier
  fixed-size-buffer-modifier fixed-size-buffer-modifiers

fixed-size-buffer-modifier:
  new
  public
  protected
  internal
  private
  unsafe

buffer-element-type:
  type

fixed-size-buffer-declarators:
  fixed-size-buffer-declarator
  fixed-size-buffer-declarator , fixed-size-buffer-declarators

fixed-size-buffer-declarator:
  identifier [ constant-expression ]

local-variable-initializer:
  ...
  stackalloc-initializer

stackalloc-initializer:
  stackalloc unmanaged-type [ expression ]

## C. 参考文献

IEEE. IEEE 二进制浮点算术标准。ANSI/IEEE 标准 754-1985。可从 http://www.ieee.org 获取。

ISO/IEC. C++。ANSI/ISO/IEC 14882:1998。

Unicode Consortium. Unicode 标准，版本 3.0。Addison-Wesley, Reading, Massachusetts, 2000, ISBN 0-201-616335-5。

本页特意留空

## 索引

A
\a 转义序列,81
抽象访问器, 46, 557-558
抽象类
  与接口, 661
  概述, 468-469
抽象事件, 566
抽象索引器, 567
抽象方法, 35, 539-540
访问和可访问性
  数组元素, 628
  包含类型, 502-503
  事件, 253
  索引器, 253, 300-301
  成员, 23-24, 107, 496
  可访问性域, 110-113
  约束, 116-117
  声明的可访问性, 107-109
  接口, 642-644
  指针, 721-722
  在主表达式中, 283-288
  protected, 113-116
  嵌套类型, 499-503
  指针元素, 723
  主表达式元素, 298-301
  属性, 252, 555-556
访问器
  抽象, 46, 557-558
  属性, 695
  事件, 564-565
  属性, 43, 46, 547-853
Acquire 语义, 514
using 语句中的获取, 445-446
add 访问器
  属性, 695
  事件, 49, 564
Add 方法
  IEnumerable, 311
  List, 42
AddEventHandler 方法, 565
加法运算符
  描述, 15
  用法, 337-340
取地址运算符, 724-725
地址
  固定变量, 728-733
  用于指针, 714, 724-725
枚举器对象的 after 状态, 593-596
Alert 转义序列,81
别名
  用于命名空间和类型, 456-461
  限定符, 464-466
  唯一性, 466
对齐枚举, 58-59
Alloc 方法, 738
分配，栈, 736-738
AllowMultiple 参数,688

+   - 歧义
+     - 语法, 287–288
+     - 在查询表达式中, 376
+   - 与号 (&)
+     - 用于地址, 716
+     - 在赋值运算符中, 389
+     - 确定性赋值规则, 188–189
+     - 用于逻辑运算符, 355–359
+     - 用于指针, 724–725
+     - 在预处理表达式中, 87
+   - AND 运算符, 15
+   - 用于类型参数的角度括号 (<>), 160
+   - 匿名函数
+     - 主体, 367
+     - 转换, 219–221
+       - 评估为委托类型, 165–166, 221–222
+       - 评估为表达式树类型, 222
+     - 实现示例, 222–226
+     - 隐式, 204
+     - 确定性赋值规则, 192
+     - 委托创建, 61
+     - 动态绑定, 369
+     - 评估, 373
+     - 表达式, 165–166, 326, 364–366
+     - 外部变量, 369–373
+     - 重载, 368
+     - 签名, 365–366
+   - 匿名对象, 317–319
+   - AppendFormat 方法, 31
+   - 可适用函数成员, 271–272
+   - 应用程序域, 99
+   - ApplicationException 类, 681
+   - 应用程序, 4
+     - 启动, 99–100
+     - 终止, 100–101
+   - Apply 方法, 60
+   - 参数, 28。另请参阅 Parameters
+     - 命令行, 99
+     - 用于函数成员, 254–259
+       - 类型, 161–162
+       - 类型推断, 259–270
+   - 算术运算符, 331–332
+     - 加法, 337–340
+     - 除法, 334–335
+   - 乘法, 332–333
+   - 指针, 725–726
+   - 余数, 336–337
+   - 移位, 344
+   - 减法, 340–342
+   - ArithmeticException 类, 335, 685
+   - 数组和数组类型, 625
+     - 访问, 299–300, 628
+     - 内容, 13
+     - 转换, 200
+     - 协变, 200, 629–630
+     - 创建, 628
+     - 描述, 8, 155
+     - 元素, 53, 171, 628
+     - 与 foreach, 429
+     - IList 接口, 627–628
+     - 初始化器, 55, 630–632
+     - 成员, 106, 628
+     - new 运算符, 53, 55, 312–315
+     - 概述, 53–55
+     - 参数, 31, 528–531
+     - 和指针, 719–720, 730–731
+     - 秩说明符, 625–626
+     - 语法语法, 804–805
+   - ArrayTypeMismatchException 类
+     - 描述, 685
+     - 类型不匹配, 390–391, 629
+   - as 运算符, 353–355
+   - 程序集, 4–5
+   - 赋值
+     - 在类与结构中, 612
+     - 确定。另请参阅 Definite assignment
+     - 固定大小缓冲区, 736
+   - 赋值运算符, 16
+     - 复合, 393–394
+     - 事件, 394–395
+     - 概述, 389–390
+     - 简单, 390–393
+   - 运算符结合性, 238–240
+   - 星号 (*)
+     - 赋值运算符, 389
+     - 注释, 69–70, 741–742
+     - 乘法, 332–333
+     - 指针, 713–716, 721
+     - 透明标识符, 385
