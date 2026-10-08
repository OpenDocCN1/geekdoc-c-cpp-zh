

## 10.2 时间类学习：抛出异常

### SetTime 方法与抛出异常

SetTime（第 13–25 行）是一个公共方法，它声明了 `int` 参数并使用这些参数来设置时间。第 16–17 行测试每个参数以确定值是否超出范围。如果所有值都在范围内，第 22–24 行将值赋值给 Hour（小时）、Minute（分钟）和 Second（秒）属性。小时（第 13 行）必须在 0 到 23 的范围内，因为世界时间格式将小时表示为0 到 23 的整数（例如，下午 1 点是 13 点，下午是 23 点；午夜是 0，正午是 12）。同样，分钟和秒都必须在 0 到 59 的范围内。对于超出范围的值，第 19 行会抛出一个 `ArgumentOutOfRangeException` 类型的异常（命名空间 System），这通知客户端向方法传递了无效参数。正如第 8 章所学到的，你可以尝试 `try...catch` 来捕获异常并从中恢复，我们在 10.2 中就是这样做的。`throw` 语句（第 19 行）创建了一个新的 `ArgumentOutOfRangeException` 对象。类名后的括号表示调用 `ArgumentOutOfRangeException` 构造函数。异常被创建后，`throw` 语句立即终止 `SetTime` 方法，并将异常返回给调用它的代码，在那里异常可以被捕获并处理。

### ToUniversalString 方法

ToUniversalString（第 28–29 行）是一个表达式方法——它没有返回语句。该方法不接受参数并返回一个世界时间格式的字符串，由六个数字组成——两个用于小时，两个分钟，两个用于秒。例如，如果时间是下午 1:30:07，ToUniversalString 方法将返回 13:30:07。该方法隐式地返回第 29 行中字符串插值表达式的值。`D2` 格式指定符将整数格式化为两位，并在需要时（如果整数不足两位）前补前导 0。

### ToString 方法

ToString（第 32–34 行）是一个表达式方法，它不接受参数并返回 Hour 中的字符串。分钟和秒的值之间用冒号分隔，并后跟 AM 或 PM 指示（例如，1:27:06 PM）。与 ToUniversalString 类似，ToString 方法返回字符串插值表达式的值。在这种情况下，我们不格式化小时，但将分钟和秒格式化为带有前导 0 的两位值。第 33 行使用条件运算符 (`:`) 来确定小时的值——如果小时为 0 或 12（AM 或 PM），它显示为 12——否则，显示为 1 到 11 之间的值。第 34 行的条件运算符决定在字符串中插入 AM 还是 PM。

## 10.2 使用 Time1 类

Time1 类（用于 10.2）创建了一个 Time1 对象并将其赋值给局部变量。`new` 算符调用了 Time1 的默认构造函数，因为 Time1 没有声明任何构造函数。第 13–17 行以世界时间格式输出第一个时间（通过调用第 14 行的 `ToUniversalString` 方法），然后以标准时间格式输出（通过调用第 16 行的 `ToString` 方法），以确认 Time1 对象已正确初始化。要更改时间，第 20 行调用了时间对象的 `SetTime` 方法。第 21–24 行再次以两种格式输出时间，以确认时间已正确设置。

### 438 第 10 章 类与对象：深度观察

```csharp
// 图 10.2: TimeTest.cs
// 在应用使用的 TimeTest 对象。
using System;

class TimeTest {
    static void Main() {
        // 创建并初始化 TimeTest 对象
        var time = new TimeTest(); // 调用 TimeTest 构造函数

        // 输出时间的字符串表示
        Console.WriteLine("\n初始世界时间是: {time.ToUniversalString()}");
        Console.WriteLine("\n初始标准时间是: {time.ToString()}");
        Console.WriteLine("\n// 输出空行");

        // 更改时间
        time.SetTime(13, 27, 6);
        Console.WriteLine("\n世界时间是: {time.ToUniversalString()}");
        Console.WriteLine("\n标准时间是: {time.ToString()}");

        // 尝试使用无效值设置时间
        try {
            time.SetTime(99, 99, 99);
        } catch (ArgumentOutOfRangeException ex) {
            Console.WriteLine(ex.Message);
        }
    }
}
```

初始世界时间是: 13:30:07
初始标准时间是: 1:30:07 PM
世界时间是: 13:27:06
标准时间是: 1:27:06 PM
指定的参数超出范围

## 10.3 控制对成员的访问

### 使用无效值调用 SetTime 方法

为了说明 SetTime 方法如何验证其参数，第 30 行使用无效的小时、分钟和秒调用 SetTime。由于类内部使用的实际数据表示方式对客户端并不重要。例如，让 Time 在内部将时间表示为午夜以来的秒数是完全合理的。客户端可以使用公共方法和属性获取结果，而无需感知这一点——练习 10.4 要求用户用午夜以来的秒数来表示时间，确实对客户端来说没有变化。

