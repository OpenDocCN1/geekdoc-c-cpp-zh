
前置递增表达式：
    ++ 一元表达式

前置递减表达式：
    -- 一元表达式

强制转换表达式：
    ( 类型 ) 一元表达式

乘法表达式：
    一元表达式
    乘法表达式 * 一元表达式
    乘法表达式 / 一元表达式
    乘法表达式 % 一元表达式

加法表达式：
    乘法表达式
    加法表达式 + 乘法表达式
    加法表达式 - 乘法表达式

移位表达式：
    加法表达式
    移位表达式 << 加法表达式
    移位表达式 right-shift 加法表达式

关系表达式：
    移位表达式
    关系表达式 < 移位表达式
    关系表达式 > 移位表达式
    关系表达式 <= 移位表达式
    关系表达式 >= 移位表达式
    关系表达式 is 类型
    关系表达式 as 类型

相等表达式：
    关系表达式
    相等表达式 == 关系表达式
    相等表达式 != 关系表达式

与表达式：
    相等表达式
    与表达式 & 相等表达式

异或表达式：
  与表达式
  异或表达式 ^ 与表达式

或表达式：
  异或表达式
  或表达式 | 异或表达式

条件与表达式：
  或表达式
  条件与表达式 && 或表达式

条件或表达式：
  条件与表达式
  条件或表达式 || 条件与表达式

null 合并表达式：
  条件或表达式
  条件或表达式 ?? null 合并表达式

条件表达式：
  null 合并表达式
  null 合并表达式 ? 表达式 : 表达式

lambda 表达式：
  匿名函数签名 => 匿名函数体

匿名方法表达式：
  delegate 显式匿名函数签名_opt 块

匿名函数签名：
  显式匿名函数签名
  隐式匿名函数签名

显式匿名函数签名：
  ( 显式匿名函数参数列表_opt )

显式匿名函数参数列表：
  显式匿名函数参数
  显式匿名函数参数列表 , 显式匿名函数参数

显式匿名函数参数：
  匿名函数参数修饰符_opt 类型 标识符

匿名函数参数修饰符：
  ref
  out

隐式匿名函数签名：
  ( 隐式匿名函数参数列表 )_opt
  隐式匿名函数参数

隐式匿名函数参数列表：
  隐式匿名函数参数
  隐式匿名函数参数列表 , 隐式匿名函数参数

隐式匿名函数参数：
  标识符

匿名函数体：
  表达式
  块

查询表达式：
  from 子句 查询体

from 子句：
  from 类型_opt 标识符 in 表达式

查询体：
  查询体子句列表_opt select 或 group 子句 查询延续_opt

查询体子句列表：
  查询体子句
  查询体子句列表 查询体子句

查询体子句：
  from 子句
  let 子句
  where 子句
  join 子句
  join-into 子句
  orderby 子句

let 子句：
  let 标识符 = 表达式

where 子句：
  where 布尔表达式

join 子句：
  join 类型_opt 标识符 in 表达式 on 表达式 equals 表达式

join-into 子句：
    join 类型_opt 标识符 in 表达式 on 表达式 equals 表达式
        into 标识符

orderby 子句：
    orderby 排序列表

排序列表：
    排序
    排序列表 , 排序

排序：
    表达式 排序方向_opt

排序方向：
    ascending
    descending

select 或 group 子句：
    select 子句
    group 子句

select 子句：
    select 表达式

group 子句：
    group 表达式 by 表达式

查询延续：
    into 标识符 查询体

赋值：
    一元表达式 赋值运算符 表达式

赋值运算符：
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
    right-shift-assignment

表达式：
  非赋值表达式
  赋值

非赋值表达式：
  条件表达式
  lambda 表达式
  查询表达式

常量表达式：
  表达式

布尔表达式：
  表达式

## B.2.5 语句

语句：
  带标签语句
  声明语句
  嵌入语句

嵌入语句：
  块
  空语句
  表达式语句
  选择语句
  迭代语句
  跳转语句
  try 语句
  checked 语句
  unchecked 语句
  lock 语句
  using 语句
  yield 语句

块：
  { 语句列表_opt }

语句列表：
  语句
  语句列表 语句

空语句：
;

带标签语句：
  标识符 : 语句

声明语句：
  局部变量声明 ;
  局部常量声明 ;

局部变量声明：
  局部变量类型 局部变量声明符列表

局部变量类型：
  类型
  var

局部变量声明符列表：
  局部变量声明符
  局部变量声明符列表 , 局部变量声明符

局部变量声明符：
  标识符
  标识符 = 局部变量初始值设定项

局部变量初始值设定项：
  表达式
  数组初始值设定项

局部常量声明：
  const 类型 常量声明符列表

常量声明符列表：
  常量声明符
  常量声明符列表 , 常量声明符

常量声明符：
  标识符 = 常量表达式

表达式语句：
  语句表达式 ;

语句表达式：
  调用表达式
  对象创建表达式
  赋值
  后置递增表达式
  后置递减表达式
  前置递增表达式
  前置递减表达式

选择语句：
  if 语句
  switch 语句

if 语句：
  if ( 布尔表达式 ) 嵌入语句
  if ( 布尔表达式 ) 嵌入语句 else 嵌入语句

switch 语句：
  switch ( 表达式 ) switch 块

switch 块：
  { switch 节列表_opt }

switch 节列表：
  switch 节
  switch 节列表 switch 节

switch 节：
  switch 标签列表 语句列表

switch 标签列表：
  switch 标签
  switch 标签列表 switch 标签

switch 标签：
  case 常量表达式 :
  default :

迭代语句：
  while 语句
  do 语句
  for 语句
  foreach 语句

while 语句：
    while ( 布尔表达式 ) 嵌入语句

do 语句：
    do 嵌入语句 while ( 布尔表达式 ) ;

for 语句：
    for ( for 初始值设定项_opt ; for 条件_opt ; for 迭代器_opt ) 嵌入语句

for 初始值设定项：
    局部变量声明
    语句表达式列表

for 条件：
    布尔表达式

for 迭代器：
    语句表达式列表

语句表达式列表：
    语句表达式
    语句表达式列表 , 语句表达式

foreach 语句：
    foreach ( 局部变量类型 标识符 in 表达式 ) 嵌入语句

跳转语句：
    break 语句
    continue 语句
    goto 语句
    return 语句
    throw 语句

break 语句：
    break ;

continue 语句：
    continue ;

goto 语句：
    goto 标识符 ;
    goto case 常量表达式 ;
    goto default ;

return 语句：
    return 表达式_opt ;

throw 语句：
    throw 表达式_opt ;

try 语句：
    try 块 catch 子句列表
    try 块 finally 子句
    try 块 catch 子句列表 finally 子句

catch 子句列表：
    特定 catch 子句列表 通用 catch 子句_opt
    特定 catch 子句列表_opt 通用 catch 子句

特定 catch 子句列表：
    特定 catch 子句
    特定 catch 子句列表 特定 catch 子句

特定 catch 子句：
    catch ( 类类型 标识符_opt ) 块

通用 catch 子句：
    catch 块

finally 子句：
    finally 块

checked 语句：
    checked 块

unchecked 语句：
    unchecked 块

lock 语句：
    lock ( 表达式 ) 嵌入语句

using 语句：
    using ( 资源获取 ) 嵌入语句

资源获取：
    局部变量声明
    表达式
