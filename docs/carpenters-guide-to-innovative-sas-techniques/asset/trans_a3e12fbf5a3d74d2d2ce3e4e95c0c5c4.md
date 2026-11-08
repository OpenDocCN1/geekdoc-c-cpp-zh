
%SAVEGLOBAL 宏将在 SAS 会话终止时执行。当前定义为全局作用域的所有宏变量都会写入数据集 ADVRPT.GLOBALVARS，在那里它们可供下一次 SAS 会话使用。对于交互式会话，必须执行 ENDSAS 语句，才能触发 -TERMSTMT 选项。

```sas
%macro SaveGlobal;
  data advrpt.GlobalVars (keep=name value);
    set sashelp.vmacro(where=(scope='GLOBAL'));
  run;
%mend saveglobal;
```

### -NOWORKINIT 和 -NOWORKTERM 选项

默认情况下，WORK 位置在 SAS 会话开始时初始化，并在 SAS 会话结束时清除。通常这正是你希望发生的情况；然而，偶尔你可能希望跨 SAS 会话保留 WORK 位置。-NOWORKINIT 选项阻止 SAS 在 SAS 会话开始时初始化 WORK 位置，而 -NOWORKTERM 阻止 SAS 在 SAS 终止时清除 WORK 位置。

这两个选项彼此独立，但通常会一起使用，因为它们允许你跨会话边界保留 WORK 空间。

## 14.1.2 数据处理选项

有一些 SYSTEM 选项被误用或未充分利用。这绝不是一份详尽的列表，只是我遇到过的一些选项。其中一些只应由充分了解其使用后果的高级用户使用。

### MERGENOBY 选项

除非以非常审慎的方式进行，否则执行不带 BY 语句的 MERGE（一对一合并）可能非常危险。当无意中这样做时，结果几乎总不是所期望的。更糟的是，这些错误往往并不明显，并且可能不会在 LOG 中产生任何警告、注释或错误消息。MERGENOBY 选项可用于改变这种行为。MERGENOBY 决定当使用 MERGE 语句而没有对应的 BY 语句时应采取什么操作。

- **NOWARN**：进行合并且不发出警告（**这是默认值**）
- **WARN**：进行合并并发出警告
- **ERROR**：不进行合并，并向 LOG 写入错误

MERGENOBY=WARN 指定 ❶ 会导致向 LOG 发出警告。我认为 MERGENOBY 选项应设置为 ERROR，并且只有在出现特定迫切需求时才重置为 WARN 或 NOWARN。MERGENOBY=WARN 会在 LOG 中产生以下警告。请注意，尽管发出了警告，MERGE 仍然会进行。

```sas
options mergenoby=warn; ❶
data aemed;
  merge advrpt.ae
        advrpt.conmed;
run;
```

```text
WARNING: No BY statement was specified for a MERGE statement.
NOTE: There were 127 observations read from the data set ADVRPT.AE.
NOTE: There were 199 observations read from the data set ADVRPT.CONMED.
NOTE: The data set WORK.AEMED has 199 observations and 13 variables.
```

### 更多信息

不带 BY 的 MERGE 语句出现在第 3.1.4 节的一个“前瞻”示例中。与该示例关联的代码会更改并随后重置 MERGENOBY 选项的当前设置。

### DATASTMTCHK 选项

此选项通过限制某些数据集名称的使用，保护用户免于因遗漏分号而覆盖数据集。默认值是 COREKEYWORDS，它阻止你将数据集命名为 UPDATE、MERGE、RETAIN 或 SET。

- **COREKEYWORDS**：数据集不得使用与核心关键字对应的名称（**默认值**）
- **ALLKEYWORDS**：还排除所有可作为 SAS DATA 步语句开头的名称（即 ARRAY、DO、OUTPUT）
- **NONE**：无限制（*事实上的* V7 之前默认值）

在这个 DATA 步中，DATA 语句 2 后遗漏了分号。实际上，我们试图创建三个数据集：WORK.AE、WORK.SET 和 ADVRPT.AE。幸运的是，DATASTMTCHK 选项的 COREKEYWORDS 设置保护了我们。在 V6 中，或将该选项设置为 NONE 时，这三个数据集都会被创建为 0 个观测和 0 个变量——我们的永久数据集 ADVRPT.AE 将被抹掉！！我认为不应将此选项重置为匹配 V6 标准（DATASTMTCHK=NONE）。

```sas
data ae
set advrpt.ae;
run;
```

```text
22   data ae
23      set advrpt.ae;
     --
56
ERROR 56-185: SET is not allowed in the DATA statement when option
DATASTMTCHK=COREKEYWORDS.
     Check for a missing semicolon in the DATA statement, or use
DATASTMTCHK=NONE
```

顺便说一句，无论数据集名称如何，只要其中包含 *逻辑库引用名*，COREKEYWORDS 和 ALLKEYWORDS 值都不会标记该数据集。因此，将数据集命名为 WORK.UPDATE 是可能的，尽管其实用性值得怀疑；而如果不带 *逻辑库引用名* 将其命名为 UPDATE，则会失败。

### VALIDVARNAME 选项

VALIDVARNAME 选项用于确定有效的变量命名约定，以及如何处理变量名。

- **V6**：变量名必须符合 V6 约定（最多 8 个字符）。此选项值不再记录在文档中，但仍适用于当前版本的 SAS。
- **V7**：允许最多 32 个字符的名称，并记住变量定义时的大小写（默认值）。
- **UPCASE**：不记住也不使用大小写。
- **ANY**：允许非标准命名约定。非标准命名约定在 Base SAS 和 SAS/STAT 之外用途有限。

### VALIDVARNAME=V6 选项

```sas
options validvarname=v6;
data a;
    abcdefghig= 5;
    run;
```

当你创建必须符合 V6 命名约定的数据集时很有用。虽然对于 VALIDVARNAME 的所有其他值都可以接受，但当 VALIDVARNAME=V6 时，以下 DATA 步会失败，因为变量名超过 8 个字符。VALIDVARNAME= 选项的这个值在未来的 SAS 版本中可能不受支持。在 SAS 9.2 中，它未被包含在 VALIDVARNAME 选项的文档中。尽管 V6 值限制变量名的长度，但它不像 SAS V6 那样限制数据集名称的长度。

VALIDVARNAME= 选项在未来的 SAS 版本中可能不受支持。在 SAS 9.2 中，它未被包含在 VALIDVARNAME 选项的文档中。尽管 V6 值限制变量名的长度，但它不像 SAS V6 那样限制数据集名称的长度。

### VALIDVARNAME=ANY 选项

此设置允许来自其他来源（如 ORACLE 或 EXCEL）的变量名，这些来源不使用与 SAS 相同的命名约定。我们通过使用命名文字量来访问这些非标准变量；只要名称包含非标准字符，就需要使用命名文字量。一旦数据导入 SAS，通常建议将这些变量重命名，以符合标准 SAS 命名约定。当数据集包含使用命名文字量定义的变量以包含非标准字符时，必须始终先将 VALIDVARNAME= 设置为 ANY，然后才能使用该数据集。此外，每当你访问任何包含非标准字符的变量时，都必须始终使用命名文字量来命名该变量。

命名文字量用引号括起，引号字符串后跟字母 n。

```sas
options validvarname=any;
proc print data=aexls;
  var subject 'ae-date'n 'ae#type'n;
  run;
```

命名文字量的使用方式与其他任何变量名一样。左侧的 VAR 语句中包含三个变量。

使用 VALIDVARNAME=ANY 的应用可以通过 EXCEL 文件 E14_1_2AE.XLS 来展示。此电子表格的列标题不符合 SAS 命名标准。

|   | Subject | AE-date | AE#type |
|---|---:|---|---:|
| 2 | 201 | 24-Apr-06 | 1 |
| 3 | 202 | 15-May-06 | 2 |

可以使用 PROC IMPORT 将此 EXCEL 表转换为 SAS 数据集。由于使用了 GETNAMES=YES 选项，SAS 将尝试将列标题用作变量名。如果未先指定 VALIDVARNAME=ANY，非标准字符将被转换为下划线。

在此示例中，这不会产生很大影响；然而，可能会产生命名冲突。通过使用 VALIDVARNAME=ANY，可以确定列在 SAS 数据集（WORK.AEXLS）中将采用的名称。查看 WORK.AEXLS 的属性可以看到，SAS 正在使用这些非标准名称。

```sas
options validvarname=any;
PROC IMPORT OUT= WORK.Aexls
    DATAFILE= "gpath\\data\\E14_1_2AE.xls"
    DBMS=EXCEL REPLACE;
    SHEET="Sheet1$";
    GETNAMES=YES;
    MIXED=NO;
    SCANTEXT=YES;
    USEDATE=YES;
    SCANTIME=YES;
RUN;
```

| 列名 | 类型 | 长度 |
|---|---|---:|
| Subject | 数值 | 8 |
| AE-date | 数值 | 8 |
| AE#type | 数值 | 8 |
