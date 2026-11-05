
排序:
    表达式  排序方向_opt

排序方向:
    升序
    降序

选择或分组子句:
    选择子句
    分组子句

选择子句:
    选择  表达式

分组子句:
    分组  表达式  按  表达式

查询延续:
    进入  标识符  查询体

赋值:
    一元表达式  赋值运算符  表达式

赋值运算符:
    =
    +=
    -=
    *=
    /=
    %=
    &=
    |=
    ^=
    <<=
    右移赋值

表达式:
    非赋值表达式
    赋值

非赋值表达式:
    条件表达式
    lambda表达式
    查询表达式

常量表达式:
    表达式

布尔表达式:
    表达式

## A.3.5 语句

语句:
    标记语句
    声明语句
    嵌入语句

嵌入语句:
  块
  空语句
  表达式语句
  选择语句
  迭代语句
  跳转语句
  try语句
  checked语句
  unchecked语句
  lock语句
  using语句
  yield语句

块:
  { 语句列表_opt }

语句列表:
  语句
  语句列表 语句

空语句:
  ;

标记语句:
  标识符 : 语句

声明语句:
  局部变量声明 ;
  局部常量声明 ;

局部变量声明:
  局部变量类型 局部变量声明符

局部变量类型:
  类型
  var

局部变量声明符:
  局部变量声明符
  局部变量声明符 , 局部变量声明符

局部变量声明符:
  标识符
  标识符 = 局部变量初始化器

局部变量初始化器:
  表达式
  数组初始化器

局部常量声明:
  const 类型 常量声明符

常量声明符:
  常量声明符
  常量声明符 , 常量声明符

常量声明符:
  标识符 = 常量表达式

表达式语句:
  语句表达式 ;

语句表达式:
invocation-expression
object-creation-expression
assignment
post-increment-expression
post-decrement-expression
pre-increment-expression
pre-decrement-expression
await-expression

选择语句:
if语句
switch语句

if语句:
if ( 布尔表达式 ) 嵌入语句
if ( 布尔表达式 ) 嵌入语句 else 嵌入语句

switch语句:
switch ( 表达式 ) switch块

switch块:
{ switch节_opt }

switch节:
switch节
switch节 switch节

switch节:
switch标签 语句列表

switch标签:
switch标签
switch标签 switch标签

switch标签:
case 常量表达式 :
default :

迭代语句:
while语句
do语句
for语句
foreach语句

while语句:
while ( 布尔表达式 ) 嵌入语句

do语句:
do 嵌入语句 while ( 布尔表达式 ) ;

for语句:
for ( for初始化器_opt ; for条件_opt ; for迭代器_opt ) 嵌入语句

for初始化器:
局部变量声明
语句表达式列表

for条件:
布尔表达式

for迭代器:
语句表达式列表

语句表达式列表:
    语句表达式
    语句表达式列表 , 语句表达式
foreach语句:
    foreach ( 局部变量类型 标识符 in 表达式 ) 嵌入语句
跳转语句:
    break语句
    continue语句
    goto语句
    return语句
    throw语句
break语句:
    break ;
continue语句:
    continue ;
goto语句:
    goto 标识符 ;
    goto case 常量表达式 ;
    goto default ;
return语句:
    return 表达式_opt ;
throw语句:
    throw 表达式_opt ;
try语句:
    try 块 catch子句
    try 块 catch子句_opt finally子句
catch子句:
    特定catch子句
    特定catch子句_opt 通用catch子句
特定catch子句:
    特定catch子句
    特定catch子句 特定catch子句
特定catch子句:
    catch ( 类型 标识符_opt ) 块
通用catch子句:
    catch 块
finally子句:
    finally 块
checked语句:
    checked 块
unchecked语句:
    unchecked 块
lock语句:
    lock ( 表达式 ) 嵌入语句
using语句:
    using ( 资源获取 ) 嵌入语句

资源获取:
  局部变量声明
  表达式
yield语句:
  yield return 表达式 ;
  yield break ;

## A.3.6 命名空间

编译单元:
  extern别名指令_opt using指令_opt 全局属性_opt
  命名空间成员声明_opt

命名空间声明:
  namespace 限定标识符 命名空间体 ;_opt

限定标识符:
  标识符
  限定标识符 . 标识符

命名空间体:
  { extern别名指令_opt using指令_opt 命名空间成员声明_opt }

extern别名指令:
  extern别名指令
  extern别名指令 extern别名指令

extern别名指令:
  extern alias 标识符 ;

using指令:
  using指令
  using指令 using指令

using指令:
  using别名指令
  using命名空间指令

using别名指令:
  using 标识符 = 命名空间或类型名 ;

using命名空间指令:
  using 命名空间名 ;

命名空间成员声明:
  命名空间成员声明
  命名空间成员声明 命名空间成员声明

命名空间成员声明:
  命名空间声明
  类型声明

类型声明:
  类声明
  结构声明
  接口声明
  枚举声明
  委托声明

限定别名成员:
  标识符 :: 标识符 类型参数列表_opt

## A.3.7 类

类声明:
    属性_opt 类修饰符_opt partial_opt class 标识符 类型参数列表_opt
    类基_opt 类型参数约束子句_opt 类体 ;_opt

类修饰符:
    类修饰符
    类修饰符 类修饰符

类修饰符:
    new
    public
    protected
    internal
    private
    abstract
    sealed
    static

类型参数列表:
    < 类型参数 >

类型参数:
    属性_opt 类型参数
    类型参数 , 属性_opt 类型参数

类基:
    : 类类型
    : 接口类型列表
    : 类类型 , 接口类型列表

接口类型列表:
    接口类型
    接口类型列表 , 接口类型

类型参数约束子句:
    类型参数约束子句
    类型参数约束子句 类型参数约束子句

类型参数约束子句:
    where 类型参数 : 类型参数约束

类型参数约束:
    主要约束
    次要约束
    构造函数约束
    主要约束 , 次要约束
    主要约束 , 构造函数约束
    次要约束 , 构造函数约束
    主要约束 , 次要约束 , 构造函数约束

主要约束:
    类类型
    class
    struct

次要约束:
    接口类型
    类型参数
    次要约束 , 接口类型
    次要约束 , 类型参数

构造函数约束:
    new ( )
类体:
    { 类成员声明_opt }
类成员声明:
    类成员声明
    类成员声明 类成员声明
类成员声明:
    常量声明
    字段声明
    方法声明
    属性声明
    事件声明
    索引器声明
    运算符声明
    构造函数声明
    析构函数声明
    静态构造函数声明
    类型声明
常量声明:
    属性_opt 常量修饰符_opt const 类型 常量声明符 ;
常量修饰符:
    常量修饰符
    常量修饰符 常量修饰符
常量修饰符:
    new
    public
    protected
    internal
    private
常量声明符:
    常量声明符
    常量声明符 , 常量声明符
常量声明符:
    标识符 = 常量表达式
字段声明:
    属性_opt 字段修饰符_opt 类型 变量声明符 ;
字段修饰符:
    字段修饰符
    字段修饰符 字段修饰符
字段修饰符:
    new
    public
    protected
    internal
    private
    static
    readonly
    volatile
