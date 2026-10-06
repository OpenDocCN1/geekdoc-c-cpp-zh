

# 执行结果

```fsharp
val tuple : string * int * string = ("John", 18, "Canada")
val it : System.Type [] = [|System.String;System.Int32;System.String;|]

val it : obj = "Canada"
val it : obj [] = [|"John"; 18; "Canada"|]
val it : obj = ("Lisa", 20, "USA")
val it : bool = true

val t : System.Type = System.Tuple'2[System.Int32,System.String]
val it : obj = (1, "One")
```

## 使用与判别联合相关的函数

列表 6-115 列出了与判别联合相关的函数。示例代码展示了如何使用反射来检查类型、获取联合情况信息、获取联合字段以及创建联合类型值。

**代码列表 6-115** 针对判别联合的 F# 反射

```fsharp
// 源代码
open Microsoft.FSharp.Reflection

// 定义一个形状判别联合
type Shape =
  | Circle of double
  | Triangle of double * double
  | Rectangle of double * double

let du = Shape.Rectangle(2., 3.)

// 检查类型是否为判别联合
FSharpType.IsUnion(du.GetType())

// 获取联合情况信息
FSharpType.GetUnionCases(du.GetType())

// 获取联合字段
FSharpValue.GetUnionFields(du, du.GetType())

// 创建新的判别联合值
let caseInfo = fst <| FSharpValue.GetUnionFields(du, du.GetType())
FSharpValue.MakeUnion(caseInfo, [| 10.; 20. |])
```

# 执行结果

```fsharp
val it : bool = true
>
val it : UnionCaseInfo [] =
[|Shape.Circle {DeclaringType = FSI_0033+Shape;
  Name = "Circle"
  Tag = 0}; Shape.Triangle {DeclaringType = FSI_0033+Shape;
  Name = "Triangle"
  Tag = 1};
Shape.Rectangle {DeclaringType = FSI_0033+Shape;
  Name = "Rectangle"
  Tag = 2};]
>
val it : UnionCaseInfo obj [] =
(Shape.Rectangle {DeclaringType = FSI_0033+Shape;
  Name = "Rectangle"
  Tag = 2};[|2.0; 3.0]])
>
val caseInfo : UnionCaseInfo Shape.Rectangle
val it : obj = Rectangle (10.0,20.0)
```

## 使用与记录相关的函数

F# 记录相关的函数在列表 6-116 中所示。示例代码展示了如何使用反射来检查类型、获取记录字段、获取特定字段以及从数组创建记录。

代码列表 6-116 针对记录的 F# 反射

```fsharp
// 源代码
open Microsoft.Sharp.Reflection

type Point2D = { x : float; y : float }
let point2Record = { Point2D.x = 1.; Point2D.y = 2. }

// 检查是否为记录类型
FSharp.IsRecord(point2Record.GetType())

// 获取记录字段
FShaderType.GetRecordFields(point2Record.GetType())

// 获取一个记录字段
let fields = FSharpType.GetRecordFields(point2Record.GetType())
FSharpValue.GetRecordField(point2Record, fields.[1])

// 从数组创建记录
FSharpValue.MakeRecord(point2Record.GetType(), [|4.; 5. |])
```

# 执行结果

```fsharp
val it : bool = true
>
```

```fsharp
val it : System.Reflection.PropertyInfo [] =
[[Double x
  [Attributes = None;
   CanRead = true;
   CanWrite = false;
   CustomAttributes = seq
   [[Microsoft.FSharp.Core.CompilationMappingAttribute((MetadataFlags(4), (Int32))]];
   DeclaringType = FSI_0038+Point2D;
   GetMethod = Double get_x();
   IsSpecialName = false;
   MemberType = Property;
   MetadataToken = 362;
   Name = "x";
   PropertyType = System.Double]];
Double y
  [Attributes = None;
   CanRead = true;
   CanWrite = false;
   CustomAttributes = seq
   [[Microsoft.FSharp.Core.CompilationMappingAttribute((MetadataFlags(4), (Int32))]];
   DeclaringType = FSI_0038+Point2D;
   GetMethod = Double get_y();
   IsSpecialName = false;
   MemberType = Property;
   MetadataToken = 363;
   Name = "y";
   PropertyType = System.Double]];
```

```fsharp
val fields : System.Reflection.PropertyInfo [] = [|...|
val it : obj = fields
```

## 在 F# 中使用异常

尽管异常并不是 F# 类型，但 F# 的异常定义可能与 C# 非常不同。列表 6-117 展示了如何使用 F# 反射——具体来说如何检查类型、获取字段以及获取异常值。

**代码列表 6-117** 针对异常的 F# 反射

```fsharp
// 源代码
open Microsoft.FSharp.Reflection

exception MyException of int * int

let ex = MyException(1, 2)

// 检查是否为异常
FSharp.IsException(ex.GetType())

// 获取异常字段
FSharpType.GetExceptionFields(ex.GetType())

// 获取异常值
FSharpValue.GetExceptionFields(ex)
```

