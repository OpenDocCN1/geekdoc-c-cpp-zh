

# 精通 SAS DS2 过程：高级数据处理技术

在 DS2 数据程序中，变量的作用范围起着至关的作用：只有全局变量会被包含在 PDV（程序处理视图）中，而只有 PDV 变量才有资格成为数据程序结果的一部分。你可以使用 `DROP` 或 `KEEP` 语句从程序结果集中明确移除全局变量。具有局部作用范围的变量不包含 PDV 中，因此不需要删除它们——它们永远不会出现在程序结果集中。

例如，在接下来的 DS2 程序中，变量 `Total` 和 `Count` 被声明为全局变量并具有全局作用范围。变量 `Category` 和 `Amount` 通过 `SET` 语句引入，也具有全局作用范围。所有这些变量可以在 `RUN` 和 `TERM` 方法中引用，并且都包含在程序结果集中。

```
proc ds2;
data;
  double Total Count;
  method run();
    set crs.one_day (keep=(Payee Amount));
    Total+Amount;
    Count+1;
  end;
  method term();
    put Total= Count=;
  end;
enddata;
run;
quit;
```

SAS 日志：

| Total=7230.5 Count=6 |

**图 2.5：数据程序生成的报告**

| Obs | Total | Payee | Amount |
|---|---|---|---|
| 1 | 9.60 | 1 Misc | $9.60 |
| 2 | 19.91 | 2 Ice Cream | $10.31 |
| 3 | 37.91 | 3 Services | $18.00 |
| 4 | 230.50 | 4 Big Retailer | $192.59 |
| 5 | 3230.50 | 5 Misc | $3,000.00 |
| 6 | 7230.50 | 6 Misc | $4,000.00 |

在下一个 DS2 程序中，变量 `Total` 和 `Count` 在 `RUN` 方法中被声明为局部的。因此，它们的作用范围局限于 `RUN`，且只能被 `RUN` 方法引用。当 `TERM` 方法尝试引用变量 `Total` 和 `Count` 时，它们在 PDV 中，因此 DS2 编译器将这些视为新的、未声明的变量。SAS 日志中产生了警告信息，并且由于未声明的变量具有全局作用范围，`Total` 和 `Count` 被包含在 PDV 和程序结果集中。然而，由于这些变量的全局变量从未被赋予值，`Total` 和 `Count` 在输出中包含缺失值：

```
proc ds2;
data;
  method run();
    declare double Total Count;
    set crs.one_day (keep=(Payee Amount));
    Total+Amount;
    Count+1;
  end;
  method term();
    put Total= Count=;
  end;
enddata;
run;
quit;
```

SAS 日志：
Total=. Count=.
WARNING: Line nn: No DECLARE for referenced variable total; creating it as a global variable of type double.
WARNING: Line nn: No DECLARE for referenced variable count; creating it as a global variable of type double.

图 2.6：数据程序生成的包含缺失值的报告

| Obs | Payee | Amount | Total | Count |
|---|---|---|---|---|
| 1 | Misc | $9.60 | . | . |
| 2 | Ice Cream | $10.31 | . | . |
| 3 | Services | $18.00 | . | . |
| 4 | Big Retailer | $192.59 | . | . |
| 5 | Misc | $3,000.00 | . | . |
| 6 | Misc | $4,000.00 | . | . |

如果我们从程序中删除 `TERM` 方法，对变量 `Total` 和 `Count` 的唯一引用就是 `RUN` 方法中的局部变量，它们将完全不会包含在 PDV 中。SAS 日志中不会发出关于未声明变量的警告，结果集仅包含全局变量 `Payee` 和 `Amount`：

```
proc ds2;
data;
  method run();
    declare double Total Count;
    set crs.one_day (keep=(Payee Amount));
    Total+Amount;
    Count+1;
  end;
enddata;
run;
quit;
```

图 2.7：排除了局部变量的数据程序生成的报告

| Obs | Payee | Amount |
|---|---|---|
| 1 | Misc | $9.60 |
| 2 | Ice Cream | $10.31 |
| 3 | Services | $18.00 |
| 4 | Big Retailer | $192.59 |
| 5 | Misc | $3,000.00 |
| 6 | Misc | $4,000.00 |

用户定义方法可以接收参数。按值传递的参数被视为方法内部的变量。例如，在下面的程序中，用户定义的 `fullname` 有两个参数 `first` 和 `last`，它们作为局部变量。这里还有一个局部声明变量 `FinalText`。主数据程序有三个全局声明变量 `WholeName`、`GivenName` 和 `Surname`。结果集仅包含这些全局变量。

```
proc ds2;
data;
  declare varchar(100) WholeName;
  method fullname(varchar(50) first, varchar(50) last)
    returns varchar(100);
    dcl varchar(100) FinalText;
    FinalText=catx(' ',last,first);
    Return FinalText;
end;
method run();
  set crs.customer_sample (keep=(GivenName Surname));
  WholeName=fullname(GivenName, Surname);
end;
enddata;
run;
quit;
```

## 第二章：DS2 语言简介

## 图 2.8：数据程序生成的报告
### 收入水平

| WholeName | GivenName | Surname |
|---|---|---|
| Schmidt, William | Schmidt | |
| Laverty, Daniel | Daniel | Laverty |
| Grayson, Sarah | Sarah | Grayson |
| Hastings, Eldon | Hastings | |

如果你曾经为了在 SAS 程序文件中存储代码片段以包含在传统的 DATA 步中，你可能经历过我所说的“PDV 污染”。当包含的代码引用了主程序中已经存在的变量，或者当包含的代码创建了主程序中不存在的变量时，它就会被添加到 PDV 中。这通常被称为 PDV 污染。

当使用 DS2 方法时，局部变量是被封装的，不会影响 PDV。在随后的章节中，我们将讨论如何利用这一特性来避免意外的数据问题。

