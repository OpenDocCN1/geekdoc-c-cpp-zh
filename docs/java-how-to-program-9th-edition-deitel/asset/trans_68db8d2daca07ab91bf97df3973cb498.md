

## G.7 打印日期和时间

转换字符 t（或 T）用于按各种格式打印日期和时间。它后面总是跟着一个指定日期和/或时间格式的转换后缀字符。当使用转换字符 T 时，输出以大写字母显示。图 G.6 列出了用于格式化同时显示日期和时间的日期/时间组合的常见转换后缀字符。图 G.7 列出了用于格式化日期的常见转换后缀字符。图 G.8 列出了用于格式化时间的常见转换后缀字符。有关转换后缀字符的完整列表，请访问 java.sun.com/javase/6/docs/api/java/util/Formatter.html。

| 转换后缀字符 | 描述 |
| :--- | :--- |
| c | 显示日期和时间，格式为“星期 月份 日期 时:分:秒 时区 年份”，其中星期和月份各三个字符，日期、时、分、秒各两位，年份四位——例如，Wed Mar 03 16:30:25 GMT-05:00 2004。使用 24 小时制。GMT-05:00 是时区。 |
| F | 显示日期，格式为“年-月-日”，年份四位，月份和日期各两位（例如，2004-05-04）。 |
| D | 显示日期，格式为“月/日/年”，月、日、年各两位（例如，03/04/04）。 |
| r | 以 12 小时制显示时间，格式为“时:分:秒 上午\|下午”，时、分、秒各两位（例如，04:30:25 PM）。 |
| R | 显示时间，格式为“时:分”，时和分各两位（例如，16:30）。使用 24 小时制。 |
| T | 显示时间，格式为“时:分:秒”，时、分、秒各两位（例如，16:30:25）。使用 24 小时制。 |

| 转换后缀字符 | 描述 |
| :--- | :--- |
| A | 显示星期几的完整名称（例如，Wednesday）。 |
| a | 显示星期几的三字符名称（例如，Wed）。 |
| B | 显示月份的完整名称（例如，March）。 |
| b | 显示月份的三字符缩写名称（例如，Mar）。 |
| d | 显示月份中的日期，两位数字，必要时用前导零填充（例如，03）。 |
| m | 显示月份，两位数字，必要时用前导零填充（例如，07）。 |
| e | 显示月份中的日期，不带前导零（例如，3）。 |
| Y | 显示年份，四位数字（例如，2004）。 |
| y | 显示年份的最后两位数字，带前导零（例如，04）。 |
| j | 显示一年中的第几天，三位数字，必要时用前导零填充（例如，016）。 |

**图 G.7 | 日期格式转换后缀字符。**

| 转换后缀字符 | 描述 |
| :--- | :--- |
| H | 以 24 小时制显示小时，必要时带前导零（例如，16）。 |
| I | 以 12 小时制显示小时，必要时带前导零（例如，04）。 |
| k | 以 24 小时制显示小时，不带前导零（例如，16）。 |
| l | 以 12 小时制显示小时，不带前导零（例如，4）。 |
| M | 显示分钟，必要时带前导零（例如，06）。 |
| S | 显示秒，必要时带前导零（例如，05）。 |
| Z | 显示时区的缩写（例如，EST 代表 Eastern Standard Time，即东部标准时间，比格林尼治标准时间晚 5 小时）。 |
| p | 以小写字母显示上午或下午标记（例如，pm）。 |
| P | 以大写字母显示上午或下午标记（例如，PM）。 |

**图 G.8 | 时间格式转换后缀字符。**

图 G.9 使用转换字符 t 和 T 配合转换后缀字符，以各种格式显示日期和时间。转换字符 t 要求对应的参数是 long、Long、Calendar（包 java.util）或 Date（包 java.util）类型的日期或时间——这些类的对象都可以表示日期和时间。出于此目的，首选 Calendar 类，因为 Date 类中的一些构造函数和方法已被 Calendar 类中的构造函数和方法所取代。

```java
1  // Fig. G.9: DateTimeTest.java
2  // Formatting dates and times with conversion characters t and T.
3  import java.util.Calendar;
4
5  public class DateTimeTest
6  {
7      public static void main( String[] args )
8      {
9          // get current date and time
10         Calendar dateTime = Calendar.getInstance();
11
12         // printing with conversion characters for date/time compositions
13         System.out.printf( "%tc\n", dateTime );
14         System.out.printf( "%tF\n", dateTime );
15         System.out.printf( "%tD\n", dateTime );
16         System.out.printf( "%tr\n", dateTime );
17         System.out.printf( "%tT\n", dateTime );
18
19         // printing with conversion characters for date
20         System.out.printf( "%1$tA, %1$tB %1$td, %1$tY\n", dateTime );
21         System.out.printf( "%1$TA, %1$TB %1$Td, %1$TY\n", dateTime );
22         System.out.printf( "%1$ta, %1$tb %1$te, %1$ty\n", dateTime );
23
24         // printing with conversion characters for time
25         System.out.printf( "%1$tH:%1$tM:%1$tS\n", dateTime );
26         System.out.printf( "%1$tZ %1$tI:%1$tM:%1$tS %1$tP", dateTime );
27     } // end main
28 } // end class DateTimeTest
```

```
Wed Feb 25 15:00:22 EST 2009
2009-02-25
02/25/09
03:00:22 PM
15:00:22
Wednesday, February 25, 2009
WEDNESDAY, FEBRUARY 25, 2009
Wed, Feb 25, 09
15:00:22
EST 03:00:22 PM
```

**图 G.9 | 使用转换字符 t 和 T 格式化日期和时间。**

第 10 行调用 Calendar 的静态方法 getInstance 获取一个包含当前日期和时间的日历。第 13–17 行、第 20–22 行和第 25–26 行在 printf 语句中使用这个 Calendar 对象作为用转换字符 t 格式化的值。第 20–22 行和第 25–26 行使用可选参数索引（"1$"）来指示格式字符串中的所有格式说明符都使用参数列表中格式字符串之后的第一个参数。你将在 G.11 节中了解更多关于参数索引的内容。使用参数索引无需重复列出同一个参数。

## G.8 其他转换字符

其余的转换字符是 b、B、h、H、% 和 n。图 G.10 描述了这些字符。图 G.11 的第 9–10 行使用 %b 打印 boolean（或 Boolean）值 false 和 true。第 11 行将一个 String 与 %b 关联，因为该字符串不是 null，所以返回 true。第 12 行将一个 null 对象与 %B 关联，由于 test 为 null，因此显示 FALSE。第 13–14 行使用 %h 打印字符串 "hello" 和 "Hello" 的哈希码值的字符串表示形式。这些值可用于在 Hashtable 或 HashMap（均在第 20 章“泛型集合”中讨论）中存储或定位字符串。这两个字符串的哈希码值不同，因为一个字符串以小写字母开头，另一个以大写字母开头。第 15 行使用 %H 打印大写形式的 null。最后两个 printf 语句（第 16–17 行）使用 %% 打印字符串中的 % 字符，使用 %n 打印平台特定的换行符。

| 转换字符 | 描述 |
| --- | --- |
| b 或 B | 为 boolean 或 Boolean 的值打印 "true" 或 "false"。这些转换字符也可以格式化任何引用的值。如果引用不为 null，则输出 "true"；否则输出 "false"。当使用转换字符 B 时，输出以大写字母显示。 |
| h 或 H | 以十六进制格式打印对象哈希码值的字符串表示形式。如果对应的参数为 null，则打印 "null"。当使用转换字符 H 时，输出以大写字母显示。 |
| % | 打印百分号字符。 |
| n | 打印平台特定的换行符（例如，Windows 上的 \r\n 或 UNIX/LINUX 上的 \n）。 |

**图 G.10 | 其他转换字符。**

```java
1  // Fig. G.11: OtherConversion.java
2  // Using the b, B, h, H, % and n conversion characters.
3
4  public class OtherConversion
5  {
6      public static void main( String[] args )
7      {
8          Object test = null;
9          System.out.printf( "%b\n", false );
10         System.out.printf( "%b\n", true );
11         System.out.printf( "%b\n", "Test" );
12         System.out.printf( "%B\n", test );
13         System.out.printf( "Hashcode of \"hello\" is %h\n", "hello" );
14         System.out.printf( "Hashcode of \"Hello\" is %H\n", "Hello" );
15         System.out.printf( "Hashcode of null is %H\n", test );
16         System.out.printf( "Printing a %% in a format string\n" );
17         System.out.printf( "Printing a new line %nnext line starts here" );
18     } // end main
19 } // end class OtherConversion
```

```
false
true
true
FALSE
Hashcode of "hello" is 5e918d2
```

**图 G.11 | 使用 b、B、h、H、% 和 n 转换字符。**

