

## 3.2.2.3 所有未通过 SET 语句引入的变量都应当声明

默认情况下，未声明新变量会导致 SAS 日志产生警告。这种行为可以通过 SAS 系统选项 `DS2COND` 进行全局控制。可以使用 `PROC DS2 SCOND` 为特定的 DS2 实例覆盖该系统选项。

表 3.1：DS2SCOND 和 SCOND 选项值及其影响

| 选项设置 | 对未声明变量的影响 |
|---|---|
| NONE | 程序正常编译并执行。日志中无条目。 |
| NOTE | 程序正常编译并执行。每个声明的变量会在 SAS 日志中生成备注。 |
| WARNING (默认) | 程序正常编译并执行。每个声明的变量会在 SAS 日志中生成警告。 |
| ERROR | 每个声明的变量都会在 SAS 日志中生成错误。程序无法编译和执行。 |

以下是将系统选项 `DS2SCOND` 设置为 `ERROR` 的示例：

```
options ds2cond=ERROR;
proc ds2;
data _null;
method run();
Text='Hello, world';
x=1;
put Text= X=;
end;
ddata;
run;
quit;
```

SAS 日志：

```
ERROR: Compilation error.
ERROR: Line 92: No DECLARE for assigned-to variable text; creating it as a global variable of type char.
ERROR: Line 93: No DECLARE for assigned-to variable x; creating it as a global variable of type double.

NOTE: The SAS stopped processing this step because of errors.
```

以下是使用 `PROC DS2` 选项 `COND` 覆盖系统选项的示例：

```
options ds2cond=ERROR;
proc ds2 scond=NONE;
data _null;
method run();
Text='Hello, world';
X=1;
put Text= X=;
enddata;
run;
quit;
```

SAS 日志：

```
Text=Hello, world
NOTE: Execution succeeded. No rows affected.
```

## 3.2.2.4 PUT 语句不支持光标和指针

此 Base SAS DATA 步使用光标控制符 (@) 和换行符 (/) 在日志中写入组织整齐的信息：

```
data_null;
Text='Hello, world';
X=1;
put @7 Text = /7 X =;
```

SAS 日志：

```
Text=Hello, world
X=1
NOTE: DATA statement used (Total process time):
real time 0.00 seconds
cpu time 0.01 second
```

然而，相同的代码在 DS2 中会产生语法错误，因为 DS2 中的 `PUT` 语句不接受光标和行控制：

```
proc ds2;
data_null;
method run();
Text='Hello, world';
X=1;
put @6 Text = / @6 X=;
enddata;
run;
quit;
```

SAS 日志：

```
ERROR: Compilation error.
ERROR: Parse encountered invalid character when expecting '';
ERROR: Line 212: Parse failed: put >>> <<< 6 Text = / @6 X=;
NOTE: The SAS System stopped processing this step because of errors.
```

## 3.2.2.5 关键字是保留字

Base SAS DATA 步语言的保留字非常少。编译器通过检查上下文来决定关键字应被解释为代码还是标识符。例如，将数据集命名为 `Data` 或将变量命名为 `Character` 是完全允许的：

```
data Data;
Character='A';
put 'The character is ' Character;
run;
```

SAS 日志：The character is A

然而，相同的代码在 DS2 中会产生语法错误，因为 DS2 的所有关键字都是保留字：

```
proc ds2;
data Data/overwrite=yes;
dcl char(1) Character;
method run();
Character='A';
put 'The character is ' Character;
end;
enddata;
run;
quit;
```

SAS 日志：ERROR: Compilation error.
ERROR: Parse encountered DATA when expecting ';';
ERROR: Line 457: Parse failed: data >>> Data << /overwrite=yes;

The SAS System stopped processing this step because of errors.

遵循 ANSI SQL 标准，只有在用双引号括起关键字时，你才能将其作为标识符：

```
proc ds2;
data "Data"/overwrite=yes;
dcl char(1) "Character"
method run();
"Character"='A';
put 'The character is ' "Character";
end;
enddata;
run;
quit;
```

SAS 日志：The character is A
NOTE: Execution succeeded. One row affected.

## 3.2.2.6 DS2 使用 ANSI SQL 引用标准

在 DS2 中，双引号仅用于界定标识符。单引号则用于界定

```
proc ds2;
data _null;
dcl char(25) "Character";
method run();
  "Character"='This is the message.';
  put "Character";
end;
enddata;
run;
quit;
```

SAS 日志：This is the message.
NOTE: Execution succeeded. No rows affected.

当尝试解析作为宏变量全部或部分时，这一要求可能会产生问题...

