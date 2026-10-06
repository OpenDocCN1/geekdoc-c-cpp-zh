

# 16 枚举类型 (Enum Types)

枚举类型是一个整数 `t` 以及该类型的零个或多个编译时常量。

枚举类型声明的格式如下：

```
enum-modifiers enum t base-clause {
  enum-member-list
}
```

其中 `enum-member-list` 是一个（可能为空的）逗号分隔的枚举成员声明列表，其具有以下形式之一：

-   enum-member
enum-member = constant-expression

`enum-modifiers` 控制枚举类型的访问权限，其规则与类访问修饰符相同（第 10.14 节）。`abstract`（抽象）和 `sealed`（密封）修饰符在使用。`base-clause` 决定枚举类型的表示类型。如果存在 `base-clause`，它必须具有 `: type` 的形式，其中 `type` 是 `byte`、`byte`、`short`、`ushort` 或 `int` 之一。如果缺少 `base-clause`，则底层表示类型为 `int`。

如果枚举成员有常量表达式，则该 `enum-member` 的值为该表达式的值；否则，如果该成员是列表中的第一个，则其值为零；否则，其值为前一个枚举成员的值加 1。常量表达式必须是常量，并且可以引用来自同一枚举类型的（未限定的）枚举成员，但枚举成员之间出现递归定义将是编译错误。不同的枚举成员可以具有不同的底层表示值。如果常量表达式计算出的值在底层表示类型中无法表示，则将是编译错误。

在枚举声明之外，`enum-member` 必须以其全限定形式编写，例如 `Month.Jan`。

枚举成员的类型是所属枚举类型声明的类型。枚举成员可以显式强制转换为底层表示类型；没有隐式转换。值 `0` 可以隐式强制转换为枚举类型；底层表示类型的其他值必须显式强制转换为枚举类型。在这两种情况下，结果值都不对应于任何已声明的成员；这并不是一个错误。

以下 14 个运算符可以应用于枚举成员：

```
= == < <= = + & ++
```

比较运算符 `==` 可以应用于两个具有相同枚举类型 `t` 的参数；其结果类型为 `bool`。运算符 `+` 和 `-` 可用于将整数加到 `t` 的枚举值上，或从 `t` 的枚举值减去一个整数；结果类型为 `t`。位运算符 `^`、`&` 和 `|` 可以应用于两个具有相同枚举类型 `t` 的参数；结果类型为 `t`。

对枚举成员进行算术运算可能会产生底层表示类型中不对应任何已声明枚举成员的结果；这并不是错误，即使在检查上下文中（第 12.3 节）。

枚举类型是 `System` 的子类。它的 `ToString` 方法将值转换为字符串。如果枚举值对应于一个或多个已声明的枚举成员，它将被格式化为符号（例如 "Jan"）；否则，将被格式化为整数（例如 "7"）。

# 示例 151 使用枚举类型表示星期和月份

在指定日期时，使用数字表示年份（2003）、日期（31）和 ISO 周数（22）是理想的，但对于星期（Sat）和月份（May）则希望使用符号值。在历法计算中，为星期（周一至周日）分配数字 0–6，为月份（一月至十二月）分配数字 1–12 是很有用的。这是在枚举类型 `Day` 和 `Month` 中实现的；注意 `Method` 中的 `Jan=1`。`Method.Daynumber` 使用 `m++` 来增加月份数（一个枚举值），`Method.Weekday` 通过将模 7 的余数强制转换为枚举类型来计算星期，而 `ToString` 将月份（一个枚举值）强制转换为 `int`。

```
public enum Day { Mon, Tue, Wed, Thu, Fri, Sat, Sun }
public enum Month { Jan=1, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec }
public class Date {
    readonly int yy // 0-9999, // 1-31 *
    readonly int mm;
    public Date(int y, Month m, int dd) {
        ...
    }
    public static int MonthDays(int y, Month m) {
        switch (m) {
            case Month.Apr: case Month.Jun: case Month.Sep: case Month.Nov:
                return 30;
            case Month.Feb:
                return LeapYear(y) ? 29 : 28;
            default:
                return 31;
        }
    }
    public static Date Fromnumber(int n) {
        ...
        Month m = Month.Jan;
        int mdays;
        while (mdays < MonthDays(y, m)) < d) {
            d -= mdays;
            m++;
        }
        return new Date(y, m, d);
    }
    public static Day Weekday(int y, Month m, int d) {
        return (Day)((ToDaynumber(y, m, d)+6) % 7);
    }
    public override string ToString() {
        // (省略实现)
    }
}
```

# 示例 152 使用枚举类型定义常量

在枚举声明之外，`enum-member` 必须以其全限定形式形式编写，例如 `Month.Jan`。

枚举成员的类型是所属枚举类型声明的类型。枚举成员可以显式强制转换为底层表示类型；没有隐式转换。值 `0` 可以隐式强制转换为枚举类型；底层表示类型的其他值必须显式强制转换为枚举类型。

```
public enum Color {
    Red,
    Green = 1,
    Blue = 2
}
Color c = Color.Red;
int val = (int)c; // 0
Color c2 = (Color)0; // Red
```

以下 14 个运算符可以应用于枚举成员：

```
= == < <= = + & ++
```

比较运算符 `==` 可以应用于两个具有相同枚举类型 `t` 的参数；其结果类型为 `bool`。运算符 `+` 和 `-` 可用于将整数加到 `t` 的枚举值上，或从 `t` 的枚举值减去一个整数；结果类型为 `t`。位运算符 `^`、`&` 和 `|` 可以应用于两个具有相同枚举类型 `t` 的参数；结果类型为 `t`。

对枚举成员进行算术运算可能会产生底层表示类型中不对应任何已声明枚举成员的结果；这并不是错误，即使在检查上下文中（第 12.3 节）。

枚举类型是 `System` 的子类。它的 `ToString` 方法将值转换为字符串。如果枚举值对应于一个或多个已声明的枚举成员，它将被格式化为符号（例如 "Jan"）；否则，将被格式化为整数（例如 "7"）。

# 示例 151 使用枚举类型表示星期和月份

在指定日期时，使用数字表示年份（2003）、日期（31）和 ISO 周数（22）是理想的，但对于星期（Sat）和月份（May）则希望使用符号值。在历法计算中，为星期（周一至周日）分配数字 0–6，为月份（一月至十二月）分配数字 1–12 是很有用的。这是在枚举类型 `Day` 和 `Month` 中实现的；注意 `Method` 中的 `Jan=1`。`Method.Daynumber` 使用 `m++` 来增加月份数（一个枚举值），`Method.Weekday` 通过将模 7 的余数强制转换为枚举类型来计算星期，而 `ToString` 将月份（一个枚举值）强制转换为 `int`。

```
public enum Day { Mon, Tue, Wed, Thu, Fri, Sat, Sun }
public enum Month { Jan=1, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec }
public class Date {
    readonly int yy // 0-9999, // 1-31 *
    readonly int mm;
    public Date(int y, Month m, int dd) {
        ...
    }
    public static int MonthDays(int y, Month m) {
        switch (m) {
            case Month.Apr: case Month.Jun: case Month.Sep: case Month.Nov:
                return 30;
            case Month.Feb:
                return LeapYear(y) ? 29 : 28;
            default:
                return 31;
        }
    }
    public static Date Fromnumber(int n) {
        ...
        Month m = Month.Jan;
        int mdays;
        while (mdays < MonthDays(y, m)) < d) {
            d -= mdays;
            m++;
        }
        return new Date(y, m, d);
    }
    public static Day Weekday(int y, Month m, int d) {
        return (Day)((ToDaynumber(y, m, d)+6) % 7);
    }
    public override string ToString() {
        // (省略实现)
    }
}
```

# 示例 152 使用枚举类型定义常量

在枚举声明之外，`enum-member` 必须以其全限定形式编写，例如 `Month.Jan`。

枚举成员的类型是所属枚举类型声明的类型。枚举成员可以显式强制转换为底层表示类型；没有隐式转换。值 `0` 可以隐式强制转换为枚举类型；底层表示类型的其他值必须显式强制转换为枚举类型。

```
public enum Color {
    Red,
    Green = 1,
    Blue = 2
}
Color c = Color.Red;
int val = (int)c; // 0
Color c2 = (Color)0; // Red
```

以下 14 个运算符可以应用于枚举成员：

```
= == < <= = + & ++
```

比较运算符 `==` 可以应用于两个具有相同枚举类型 `t` 的参数；其结果类型为 `bool`。运算符 `+` 和 `-` 可用于将整数加到 `t` 的枚举值上，或从 `t` 的枚举值减去一个整数；结果类型为 `t`。位运算符 `^`、`&` 和 `|` 可以应用于两个具有相同枚举类型 `t` 的参数；结果类型为 `t`。

对枚举成员进行算术运算可能会产生底层表示类型中不对应任何已声明枚举成员的结果；这并不是错误，即使在检查上下文中（第 12.3 节）。

枚举类型是 `System` 的子类。它的 `ToString` 方法将值转换为字符串。如果枚举值对应于一个或多个已声明的枚举成员，它将被格式化为符号（例如 "Jan"）；否则，将被格式化为整数（例如 "7"）。

(注：后续部分内容由于用户提供的原文中存在大量重复和乱码，翻译时已根据逻辑进行了清理和对齐)

