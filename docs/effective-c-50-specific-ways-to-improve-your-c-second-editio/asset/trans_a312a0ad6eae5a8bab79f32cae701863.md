
StringBuilder 类, 97–98
String.Format(), 97
条纹分区, 205–206
强异常保证, 284–294
强类型, 12
结构体
  接口实现, 137–138
  GetHashCode() 的陷阱, 47
  理解相等性和关系, 36–44
结构体与类, 104–110
可替代性
  与转换运算符, 56–60
  协变和逆变, 171–177
子系统添加, 150–152
支持
  泛型协变和逆变, 171–177
  ICloneable, 194
  IComparable, 184–185
  IFormattable.ToString(), 33
  用于序列化的类型, 157–166
Sutter, Herb, 285
相等性的对称性, 38
语法，查询与循环, 51–56
System.Array, 44
System.Collections.ObjectModel.ReadOnlyCollection<T>, 157
System.Diagnostics.Debug, 23
System.Diagnostics.Trace, 23
System.Exception, 281–282
System.Linq.Enumerable 类, 131–134
System.Linq.Enumerable.Cast<T>, 236–239
System.Linq.Expression 类, 230
System.Object, 275–279
System.Object.ToString(), 28–36
T
Take(), 213–214
Task 类, 217–219
测试, 129
文本表示, 28–36
This, 6
this(), 85
抛出异常
  创建异常类, 281
  强异常保证, 284–294
ToString(), 28–36
TRACE 环境变量, 26–28
Trace.WriteLine, 24
事务优化, 166–171
相等性的传递性, 38
翻译，异常, 284
TrueForAll(), 144–145
try/catch, 224–225
try/finally, 87–94
TryGetIndex, 248–249
TryGetMember, 244–245, 248
TrySetMember, 244–245
Tuple<> 类, 44
类型
  避免在 API 中使用转换运算符, 56–60
  检查, 12
  定义和实现接口与继承, 129–138
  区分值类型和引用类型, 104–110
  使用 IComparable<T> 和 IComparer<T> 实现排序关系, 183–190
  限制可见性, 126–129
  使其可序列化, 157–166
  GetHashCode() 的陷阱, 44–51
  优先使用 is 或 as 运算符而不是强制转换, 12–20
  dynamic 的优缺点, 227–236
  提供 ToString(), 28–36
  引用类型。参见 引用类型
  支持泛型协变和逆变, 171–177
  理解相等关系, 36–44
  使用编译时与运行时常量, 8–9
  使用 dynamic 处理接收匿名类型的参数, 239–243
  使用 DynamicObject 或 IDynamicMetaObjectProvider 实现数据驱动的动态, 243–254
  值类型。参见 值类型

U
一元运算符, 245–246
拆箱操作
  最小化, 275–279
  结构体, 137–138
单元测试, 129
非托管资源
  避免不必要的对象创建, 94–98
  为其创建终结器, 99–100, 104
  释放, 87–94

无关类型, 135–137
更新
  编译时与运行时常量, 10
  仅在对基类做出反应时使用 new, 194–198
UsedMemory, 264–266
用户定义转换
  利用泛型类型参数的运行时类型, 237–238
  优先使用 is 或 as 而不是强制转换, 13–15
用户定义类型
  以文本形式显示, 28–36
  优先使用 is 或 as 而不是强制转换, 14–15
  使用
    隐式, xv–xvi
    用于资源清理, 87–94

V
值类型
  避免 ICloneable, 191
  区分引用类型和值类型, 104–110
  确保 0 是有效状态, 110–114
  表达相等性, 36–44
  foreach 支持与强制转换, 18
  最小化装箱和拆箱, 275–279
  GetHashCode() 的陷阱, 44–51
  优先使用不可变原子类型, 114–123
  防止被修改, 155
  与编译时常量一起使用, 8–9
ValueType.Equals(), 38–39
ValueType.GetHashCode(), 46–48

变量初始化, 74–77

方差支持, 171–177

版本
  使用编译时常量存储, 10–11
  类型序列化, 157–166
  何时使用 new 修饰符, 196–198

虚函数
  用于释放, 100
  new 修饰符与, 195–196

虚方法
  接口方法与之有何不同, 139–143
  重写, 179–182
  使用重写代替事件处理程序, 179–182

虚属性, 3–4

可见性，限制类型, 126–129

Vlissides, John M., 146, 240

Void 返回类型, 27

## W

Wagner, Bill, xvii–xviii

Web 服务
  创建大粒度互联网服务 API, 166–171
  使用表达式 API 改进, 255–257

WithDegreeOfParallelism(), 214

WithExecutionMode(), 214

WithMergeOptions(), 214

包装器
  动态对象, 268–269
  信封-信件模式, 288–293
  防止只读属性被修改, 157

## X

XAML 声明, 182

XML，LINQ to XML, 244–245
