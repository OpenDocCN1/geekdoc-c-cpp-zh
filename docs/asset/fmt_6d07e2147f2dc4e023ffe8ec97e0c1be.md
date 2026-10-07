
- `LEADING` – 这是一个可选参数。从字符串的开头移除 `trim_character`。
- `TRAILING` – 这是一个可选参数。从字符串的末尾移除 `trim_character`。
- `BOTH` – 这是一个可选参数。从字符串的开头和结尾都移除 `trim_character`。

`trim_character FROM` – 这是一个可选参数。将从字符串中移除的字符。如果省略此参数，它将移除字符串中的空格字符。

- `string` – 要进行修剪的字符串。

如果你没有为第一个参数（`LEADING`, `TRAILING`, `BOTH`）指定值，`TRIM` 函数将默认使用 `BOTH`，并从字符串的开头和结尾移除 `trim_character`。

如果你没有指定 `trim_character`，`TRIM` 函数将默认将要移除的字符视为空格。大多数人考虑使用 `TRIM` 函数时通常处于这种语境，`TRIM` 通常用于移除字符串开头和结尾的空白字符。

以下是使用 `TRIM` 的示例：

`SELECT TRIM(LEADING'' FROM 'HelloThere ');`

Result: `'HelloThere '`

```
SELECT TRIM(TRAILING '' FROM ' HelloThere ');
Result: ' HelloThere'
SELECT TRIM(BOTH '' FROM ' HelloThere ');
Result: 'HelloThere'
```

```
SELECT TRIM(' ' FROM 'HelloThere ');
Result: HelloThere
```

```
SELECT TRIM(' HelloThere ' ');
Result: 'HelloThere'
```

```
SELECT TRIM(LEADING '0' FROM '000123');
Result: '123'
```

```
SELECT TRIM(TRAILING '1' FROM 'Hello1');
Result: 'Hello'
```

```
SELECT TRIM(BOTH '123' FROM '123Hello123');
Result: 'Hello'
```

# 15.10 - LTRIM

MySQL `LTRIM` 函数用于从字符串的左侧所有所有空格字符。

`LTRIM` 的语法如下：

```
LTRIM ( string )
```

`string` – 要从左侧移除空格字符的字符串。

以下是使用 `LTRIM` 的示例：

```
SELECT LTRIM(' HelloThere');
Result: 'HelloThere'

SELECT LTRIM(' Hello how are you ');
Result: 'Hello how are you '
```

# 15.11 - RTRIM

MySQL `RTRIM` 函数用于从字符串的右侧移除所有空格字符。它的功能与 `LTRIM` 相同；但是，它是在字符串的相反侧执行此操作。

`RTRIM` 的语法如下：

```
RTRIM ( string )
```
`string` – 要从左侧移除空格字符的字符串。

以下是使用 `RTRIM` 的示例：

```
SELECT RTRIM ('HelloThere ');
Result: 'HelloThere '
```

```
SELECT RTRIM (' Hello how are you ');
Result: ' Hello how are you '
```

# 15.12 - UPPER

MySQL `UPPER` 函数将指定字符串中的所有字符转换为大写。如果字符串中包含不是字母的字符，这些字符不受此函数的影响。

`UPPER` 的语法如下：

```
UPPER( string )
```
`string` – 要转换为大写的字符串。

`UPPER` 函数将使用当前的字符映射集转换字符，默认认为 `latin1`。`UCASE` 函数是 `UPPER` 函数的同义词。

以下是使用 `UPPER` 的示例：

```
SELECT UPPER(Hello how are You);
Result: 'HELLO HOW ARE YOU'
```

```
SELECT UPPER('hello there 123');
Result: 'HELLO THERE 123 '
```

# 15.13 - LOWER

MySQL `LOWER` 函数将指定字符串中的所有字符转换为小写。如果字符串中包含不是字母的字符，这些字符不受此函数的影响。该函数可以被视为 `UPPER` 的相反操作。

`LOWER` 的语法如下：

```
LOWER ( string )
```
`string` – 要转换为小写的字符串。

`LOWER` 函数将使用当前的字符映射集转换字符，默认认为 `latin1`。`LCASE` 函数是 `LOWER` 函数的同义词。

以下是使用 `LOWER` 的示例：

```
SELECT LOWER(Hello how are You);
Result: 'hello how are you'
```

```
SELECT UPPER(HELLO THERE 123');
Result: 'hello there 123 '
```

## 第 16 章：数值函数

# 16.1 – ABS

MySQL `ABS` 函数返回数字的绝对值。“绝对值”会移除数字前的任何负号，并将所有数字评估为正数（或零）。

`ABS` 的语法如下：

```
ABS( number )
```
`number` – 要转换为绝对值的数字。

以下是使用 `ABS` 的示例：

```
SELECT ABS(-30);
Result: 30
```

```
SELECT ABS(30.5);
Result: 30.5
```

```
SELECT ABS(-30.5);
Result: 30.5
```

```
SELECT ABS(30);
Result: 30
```

# 16.2 – CEILING

MySQL `CEILING` 函数返回大于或等于数字的最小整数。`CEIL` 函数是 `CEILING` 的同义词。

`CEILING` 的语法如下：

```
CEILING( number )
```
`number` – 要转换为最小整数的数字。

以下是使用 `CEILING` 的示例：

```
SELECT CEILING(30);
Result: 30
```

```
SELECT CEILING(30.5);
Result: 31
```

```
SELECT CEILING(-30);
Result: -30
```

```
SELECT CEILING(-30.5);
Result: -30
```

# 16.3 – FLOOR

MySQL `FLOOR` 函数返回小于或等于数字的最大整数。该函数可以被视为 `CEILING` 的相反操作。

`FLOOR` 的语法如下：

```
FLOOR( number )
```
`number` – 要转换为最大整数的数字。

以下是使用 `FLOOR` 的示例：

```
SELECT FLOOR(30);
Result: 30
```

```
SELECT FLOOR(30.5);
Result: 30
```

```
SELECT FLOOR(-30);
Result: -30
```

```
SELECT FLOOR(-30.5);
Result: -31
```

# 16.4 – ROUND

MySQL `ROUND` 函数将数字按指定的位数四舍五入。

`ROUND` 的语法如下：

```
ROUND(number, [ decimal_places ] )
```
`number` – 要舍入的数字。
`decimal_places` – 舍入的位数。此值必须是正负整数。如果省略此参数，`ROUND` 函数将数字四舍入到 0 位。

以下是使用 `ROUND` 的示例：

```
SELECT ROUND(10.455);
Result: 10.46
```

```
SELECT ROUND(10.415, 0);
Result: 10
```

```
SELECT ROUND(10.415, 1);
Result: 10.4
```

```
SELECT ROUND(10.415, 2);
Result: 10.42
```

```
SELECT ROUND(-10.415);
Result: -10
```

```
SELECT ROUND(-10.615);
Result: -11
```

# 16.5 - MOD

MySQL `MOD` 函数返回 `n` 除以 `m` 的余数。`MOD` 代表模。如果你是初学者，之前可能还没有见过模运算符。

使用 `MOD` 函数获取两个数字相除后的余数。例如，`12 MOD 5` 等于 `2`。`MOD` 函数对于需要固定行数并想知道剩余行数的情况非常有用。假设你有一个在线商店，每页显示 10 个产品。现在有 18 个产品。你可以使用 `MOD` 函数来确保当用户导航到结果第二页时，只检索剩余的 8 个产品。`MOD` 的语法如下：

`n MOD m`

OR

`MOD( n, m )`

OR

`n % m`（注意：`%` 是 `MOD` 的运算符）

以上三种语法都是有效的。

`n` – 被除的值。
`m` – 除入 `n` 的值。

以下是使用 `MOD` 的示例：

```
SELECT MOD(12, 5);
Result: 2
```

```
SELECT 12 % 5;
```

结果: 2

## 16.6 - SQRT

MySQL `SQRT` 函数返回一个数字的平方根。

`SQRT` 的语法如下：

```
SQRT( number )
```

参数或参数值
- `number` – 你想要获取平方根的正数

如果数字为负值，`SQRT` 函数返回 `NULL`。
以下是一些使用 `SQRT` 的示例：

```
SELECT SQRT(25);
Result: 5
```

```
SELECT SQRT(26);
Result: 5.099019513592785
```

```
SELECT SQRT(0);
Result: 0
```

```
SELECT SQRT(-9);
Result: NULL
```

## 第17 章：日期函数

## 17.1 - ADDDATE

MySQL `ADDDATE` 函数返回增加某个时间间隔后的日期。

`ADDDATE` 的语法如下：

```
ADDDATE( date, INTERVAL unit )
```

或

```
ADDDATE( date, days )
```

- `date` – 要增加的日期。
- `days` – 要增加的天数（第二种语法）。
- `value` – 要增加的时间/日期间隔。该参数可以指定正负值（第一种语法）。
- `unit` – 间隔的单位，如 `DAY`、`MONTH`、`HOUR` 等。

以下是一些使用 `ADDDATE` 的示例：

```
SELECT ADDDATE('2020-05-15', INTERVAL 10 DAY);
Result: '2020-05-25'
```

```
SELECT ADDDATE('2020-05-15', 10);
Result: '2020-05-25'
```

```
SELECT ADDDATE('2020-02-13', INTERVAL 12 WEEK);
Result: '2020-05-08'
```

```
SELECT ADDDATE('2020-02-13', INTERVAL -3 MONTH);
Result: '2019-11-13'
```

```
SELECT ADDDATE('2020-02-13', INTERVAL 3 QUARTER);
Result: '2020-11-13'
```

```
SELECT ADDDATE('2020-02-13', INTERVAL 5 YEAR);
Result: '2025-02-13'
```

## 17.2 - SUBDATE

MySQL `SUBDATE` 函数返回减去某个时间间隔后的日期。该函数可以视为 `ADDDATE` 的逆操作。

`SUBDATE` 的语法如下：

```
SUBDATE( date, INTERVAL unit )
```

或

```
SUBDATE( date, days )
```

- `date` – 要减去的日期。
- `days` – 从日期中减去的天数（第二种语法）。
- `value` – 要减的时间/日期间隔。该参数可以指定正负值（第一种语法）。
- `unit` – 间隔的类型，如 `DAY`、`MONTH`、`HOUR` 等。

以下是一些使用 `SUBDATE` 的示例：

```
SELECT SUBDATE('2020-05-15', INTERVAL 10 DAY);
Result: '2020-05-05'
```

```
SELECT SUBDATE('2020-05-15', 10);
Result: '2020-05-05'
```

```
SELECT SUBDATE('2020-02-13', INTERVAL 12 WEEK);
Result: '2019-11-21'
```

```
SELECT SUBDATE('2020-02-13', INTERVAL 3 MONTH);
Result: '2019-11-13'
```

```
SELECT SUBDATE('2020-02-13', INTERVAL 3 QUARTER);
Result: '2019-05-13'
```

```
SELECT SUBDATE('2020-02-13', INTERVAL 5 YEAR);
Result: '2015-02-13'
```

## 17.3 - ADDTIME

MySQL `ADDTIME` 返回增加某个时间间隔后的时间/日期值。

`ADDTIME` 的语法如下：

```
ADDTIME(start_value, time)
```

`start_value` – 要增加时间间隔的 `DATETIME` 值。
`time` – 要增加的时间间隔值。它可以是正值或负值。如前所述，时间的格式为 `'HH:MM:SS'`。支持的范围为 `'-838:59:59'` 到 `'838:59:59'`。

使用负值作为参数的 `ADDTIME` 函数等于使用 `SUBTIME` 函数。

以下是一些使用 `ADDTIME` 的示例：

```
SELECT ADDTIME('2020-02-13 08:44:21.000001', '0.000001');
Result: '2020-02-13 08:44:23.000002'
```

```
SELECT ADDTIME('2020-02-13 08:44:21.000001', '3:000001');
Result: '2020-02-13 11:46:21.000002'
```

```
SELECT ADDTIME('2020-02-13 08:44:21.000001', '4:00001');
Result: '2020-02-13 12:47:23.000002'
```

```
SELECT ADDTIME('2020-02-13 08:44:21.000001', '5:4:00001');
Result: '2020-02-13 13:47:23.00002'
```

```
SELECT ADDTIME('01:15:23.999998', '0.000001');
Result: '01:15:23.999999'
```

```
SELECT ADDTIME('01:15:23.999998', '5.000001');
Result: '01:15:28.999999'
```

```
SELECT ADDTIME('01:15:23.000001', '8:12:15.003441');
Result: '09:27:38.003442'
```

```
SELECT ADDTIME('01:15:23.000001', '-8:12:15.003441');
Result: '-06:56:52.003440'
```

## 17.4 - SUBTIME

MySQL `SUBTIME` 返回减去某个时间间隔后的时间/日期值。该函数可以视为 `ADDTIME` 的逆操作。

`SUBTIME` 的语法如下：

```
SUBTIME( start_value, time )
```

`start_value` – 要减去时间间隔的时间或 `datetime` 值。
`time` – 要减去的时间间隔值。可以是正数。

使用负时间值作为参数的 `SUBTIME` 函数等于使用 `ADDTIME` 函数。

以下是一些使用 `SUBTIME` 的示例：

```
SELECT SUBTIME('2020-02-13 08:44:21.000002', '2.000001');
Result: '2020-02-13 08:44:19.000001'
```

```
SELECT SUBTIME('2020-02-13 08:44:21.000002', '3:000001');
Result: '2020-02-13 05:42:21.000001'
```

```
SELECT SUBTIME('2020-02-13 08:44:21.000002', '4:00001');
Result: '2020-02-13 04:41:19.000001'
```

```
SELECT SUBTIME('2020-02-13 08:44:21.000002', '5:4:00001');
Result: '2020-02-08 04:41:19.000001'
```

```
SELECT SUBTIME('01:15:23.999998', '0.000001');
Result: '01:15:23.999997'
```

```
SELECT SUBTIME('01:15:23.999998', '5.000001');
Result: '01:15:18.999997'
```
