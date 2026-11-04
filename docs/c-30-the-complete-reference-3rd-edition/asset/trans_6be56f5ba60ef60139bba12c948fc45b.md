
| 方法 | 含义 |
|---|---|
| public static retType Parse(string str, IFormatProvider formatProvider) | 使用 formatProvider 提供的区域性特定信息，返回 str 中数字字符串的二进制等效值。如果该字符串不表示由结构类型定义的数值，则引发异常。retType 是实际返回数据类型的占位符，具体取决于所使用的数值结构。例如，对于 Int32，retType 将是 int。 |
| public static retType Parse(string str, NumberStyles styles) | 使用 styles 提供的样式信息，返回 str 中数字字符串的二进制等效值。如果该字符串不表示由结构类型定义的数值，则引发异常。retType 是实际返回数据类型的占位符，具体取决于所使用的数值结构。例如，对于 Int32，retType 将是 int。 |
| public static retType Parse(string str, NumberStyles styles, IFormatProvider formatProvider) | 使用 styles 提供的样式信息以及 formatProvider 提供的区域性特定格式信息，返回 str 中数字字符串的二进制等效值。如果该字符串不表示由结构类型定义的数值，则引发异常。retType 是实际返回数据类型的占位符，具体取决于所使用的数值结构。例如，对于 Int32，retType 将是 int。 |
| public override string ToString() | 返回调用对象值的字符串表示形式。 |
| public string ToString(string format) | 返回调用对象值的字符串表示形式，其格式由 format 传入的格式字符串指定。 |
| public string ToString(IFormatProvider formatProvider) | 使用 formatProvider 中指定的区域性特定信息，返回调用对象值的字符串表示形式。 |
| public string ToString(string format, IFormatProvider formatProvider) | 使用 formatProvider 指定的区域性特定信息以及 format 指定的格式，返回调用对象值的字符串表示形式。 |
| public static bool TryParse(string str, out type val) | 尝试将 str 中的数字字符串转换为二进制值。如果成功，则将该值存储在 val 中并返回 true。如果未进行转换，则返回 false。这与 Parse() 不同，后者在失败时引发异常。在 TryParse() 中，type 显式指定数据类型，例如在 System.Int32.TryParse(int v) 中那样。 |
| public static bool TryParse(string str, NumberStyles styles, IFormatProvider formatProvider, out type val) | 使用 styles 提供的样式信息以及 formatProvider 提供的区域性特定格式信息，尝试将 str 中的数字字符串转换为二进制值。如果成功，则将该值存储在 val 中并返回 true。如果未进行转换，则返回 false。这与 Parse() 不同，后者在失败时引发异常。在 TryParse() 中，type 显式指定数据类型，例如在 System.Int32.TryParse(int v) 中那样。 |

### 表 21-2 整数结构支持的方法（续）

## 浮点结构

有两个浮点结构：Double 和 Single。Single 表示 float。其方法见表 21-3，其字段见表 21-4。Double 表示 double。其方法见表 21-5，其字段见表 21-6。与整数结构一样，可以在调用 Parse() 或 ToString() 时指定区域性特定信息和格式信息。

浮点结构实现以下接口：IComparable、IComparable<T>、IConvertible、IFormattable 和 IEquatable<T>，其中对于 Double，T 替换为 double；对于 Single，T 替换为 float。

| 方法 | 含义 |
|---|---|
| public int CompareTo(object v) | 将调用对象的数值与 v 的数值进行比较。如果值相等，则返回零。如果调用对象的值较小，则返回负值。如果调用对象的值较大，则返回正值。 |
| public int CompareTo(float v) | 将调用对象的数值与 v 的数值进行比较。如果值相等，则返回零。如果调用对象的值较小，则返回负值。如果调用对象的值较大，则返回正值。 |
| public override bool Equals(object v) | 如果调用对象的值等于 v 的值，则返回 true。 |
| public bool Equals(float v) | 如果调用对象的值等于 v 的值，则返回 true。 |
| public override int GetHashCode() | 返回调用对象的哈希代码。 |
| public TypeCode GetTypeCode() | 返回 Single 的 TypeCode 枚举值，即 TypeCode.Single。 |
| public static bool IsInfinity(float v) | 如果 v 表示无穷大（正无穷大或负无穷大），则返回 true。否则，返回 false。 |
| public static bool IsNaN(float v) | 如果 v 不是数字，则返回 true。否则，返回 false。 |

### 表 21-3 Single 支持的方法

| 字段 | 含义 |
|---|---|
| public const float Epsilon | 最小的非零正值。 |
| public const float MaxValue | float 可容纳的最大值。 |
| public const float MinValue | float 可容纳的最小值。 |
| public const float NaN | 表示非数字的值。 |
| public const float NegativeInfinity | 表示负无穷大的值。 |
| public const float PositiveInfinity | 表示正无穷大的值。 |

### 表 21-4 Single 支持的字段

| 方法 | 含义 |
|---|---|
| public int CompareTo(object v) | 将调用对象的数值与 v 的数值进行比较。如果值相等，则返回零。如果调用对象的值较小，则返回负值。如果调用对象的值较大，则返回正值。 |
| public int CompareTo(double v) | 将调用对象的数值与 v 的数值进行比较。如果值相等，则返回零。如果调用对象的值较小，则返回负值。如果调用对象的值较大，则返回正值。 |
| public override bool Equals(object v) | 如果调用对象的值等于 v 的值，则返回 true。 |
| public bool Equals(double v) | 如果调用对象的值等于 v 的值，则返回 true。 |
| public override int GetHashCode() | 返回调用对象的哈希代码。 |
| public TypeCode GetTypeCode() | 返回 Double 的 TypeCode 枚举值，即 TypeCode.Double。 |
| public static bool IsInfinity(double v) | 如果 v 表示无穷大（正无穷大或负无穷大），则返回 true。否则，返回 false。 |
| public static bool IsNaN(double v) | 如果 v 不是数字，则返回 true。否则，返回 false。 |
| public static bool IsPositiveInfinity(double v) | 如果 v 表示正无穷大，则返回 true。否则，返回 false。 |
| public static bool IsNegativeInfinity(double v) | 如果 v 表示负无穷大，则返回 true。否则，返回 false。 |
| public static double Parse(string str) | 返回 str 中数字字符串的二进制等效值。如果该字符串不表示 double 值，则引发异常。 |
| public static double Parse(string str, IFormatProvider formatProvider) | 使用 formatProvider 提供的区域性特定信息，返回 str 中数字字符串的二进制等效值。如果该字符串不表示 double 值，则引发异常。 |
| public static double Parse(string str, NumberStyles styles) | 使用 styles 提供的样式信息，返回 str 中数字字符串的二进制等效值。如果该字符串不表示 double 值，则引发异常。 |
| public static double Parse(string str, NumberStyles styles, IFormatProvider formatProvider) | 使用 styles 提供的样式信息以及 formatProvider 提供的区域性特定格式信息，返回 str 中数字字符串的二进制等效值。如果该字符串不表示 double 值，则引发异常。 |
| public override string ToString() | 以默认格式返回调用对象值的字符串表示形式。 |
| public string ToString(string format) | 返回调用对象值的字符串表示形式，其格式由 format 传入的格式字符串指定。 |
| public string ToString(IFormatProvider formatProvider) | 使用 formatProvider 中指定的区域性特定信息，返回调用对象值的字符串表示形式。 |
| public string ToString(string format, IFormatProvider formatProvider) | 使用 formatProvider 指定的区域性特定信息以及 format 指定的格式，返回调用对象值的字符串表示形式。 |
| public static bool TryParse(string str, out double val) | 尝试将 str 中的数字字符串转换为 double 值。如果成功，则将该值存储在 val 中并返回 true。如果未进行转换，则返回 false。这与 Parse() 不同，后者在失败时引发异常。 |
| public static bool TryParse(string str, NumberStyles styles, IFormatProvider formatProvider, out double val) | 使用 styles 提供的样式信息以及 formatProvider 提供的区域性特定格式信息，尝试将 str 中的数字字符串转换为 double 值。如果成功，则将该值存储在 val 中并返回 true。如果未进行转换，则返回 false。这与 Parse() 不同，后者在失败时引发异常。 |

### 表 21-5 Double 支持的方法

