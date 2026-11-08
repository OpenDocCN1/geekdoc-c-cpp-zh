
```sas
proc summary data=advrpt.demog;
    class race edu;
    var ht; ❶
    output out=stats
             mean=
             stderr=
             min=/autoname; ❷
run;

proc print data=stats;
    id race edu;
    var ht_; ❸
run;
```

❶ 分析变量 HT 和 WT 用于生成一系列统计量。这些统计量的名称会自动生成 ❷，形式为 *分析变量_统计量*（关于 AUTONAME 选项的更多详细信息见第 7.2 节）。

❸ 为 HT 变量生成的所有统计量列表将使用 VAR 语句中的名称前缀列表打印。

### 更多信息

这个列表缩写用于第 2.5.2 节中的一个 PROC TRANSPOSE 示例。

### 特殊名称列表

存在三种名称列表，允许你按变量类型来引用变量。它们包括：

- `_CHARACTER_` — 所有字符变量
- `_NUMERIC_` — 所有数值变量
- `_ALL_` — PDV 上的所有变量

由于这些列表中的每一个都针对当前变量列表，因此它们不会创建变量。在每种情况下，生成的变量列表将与它们在程序数据向量（Program Data Vector）上的顺序相同。

`_ALL_` 列表缩写用于下面的 DATASETS 步骤中，以从数据集中移除标签和格式属性。此示例由 SAS Sample #25052 提供。

```sas
proc datasets lib=work nolist;
    modify demog;
        attrib _all_ label=' '
                     format=;
        contents;
quit;
```

MODIFY 语句打开 WORK.DEMOG 数据集，并且通过使用 `_ALL_` 列表缩写列出变量，将 ATTRIB 语句应用于该数据集的所有变量。

### 另请参阅

可在 http://support.sas.com/kb/25/052.html 的 SAS Sample 库中找到此示例及进一步说明。

## 2.6.2 理解 ORDER= 选项

ORDER= 选项可用于大多数对数据进行分类或汇总的过程。它使我们无需物理排序数据即可控制信息的分析顺序和显示顺序。根据过程的不同，该选项可应用于 PROC 语句或一个或多个支持语句（如 CLASS 语句）。

该选项可取以下值：

| 选项值 | 排序依据 |
| --- | --- |
| INTERNAL | 未格式化的值（类似于 PROC SORT） |
| FORMATTED | 格式化后的值 |
| FREQ | 降序频数 |
| DATA | 数据值的顺序 |

对于大多数过程，ORDER= 的默认值为 INTERNAL。

在以下每个示例中，使用带单个分类变量（SYMP）的简单 PROC MEANS 来演示 ORDER= 选项的效果。

### ORDER=INTERNAL

这通常是变量使用 PROC SORT 排序后的顺序，并且通常是该过程的默认值。其别名为 UNFORMATTED。

```sas
    title2 'order=internal';
    proc means data=advrpt.demog
      n mean;
      class symp;
      var ht;
    run;
```

未指定 ORDER= 选项，并且 PROC MEANS 对所有分类变量的默认顺序为 ORDER=INTERNAL。因此，症状按字母顺序出现（SYMP 是字符型）。

**2.6.2 理解 ORDER=**
**order=internal**

**MEANS 过程**

*分析变量：ht 身高（英寸）*

| 症状代码 | N 观测 | N | 均值 |
| --- | --- | --- | --- |
| 01 | 4 | 4 | 67.5000000 |
| 02 | 10 | 10 | 66.8000000 |
| 03 | 4 | 4 | 66.5000000 |
| 04 | 13 | 13 | 68.6923077 |
| 05 | 8 | 8 | 67.5000000 |
| 06 | 11 | 11 | 64.0000000 |
| 09 | 2 | 2 | 68.0000000 |
| 10 | 13 | 13 | 68.5384615 |

### ORDER=FORMATTED

当使用 ORDER=FORMATTED 选项时，值会先格式化，然后再排序。

### ORDER=DATA

分类变量的顺序将反映它们在数据本身中的顺序。检测到的第一个水平将最先写出。数据不必按任何特定顺序排列。

```sas
    title2 'order=data';
    proc means data=advrpt.demog
         n mean
         order=data;
       class symp;
       var ht;
    run;
```

症状 02（咳嗽）是数据中的第一个症状，随后是 10 和 06。

### 更多信息

分类变量的缺失值通常不会包含在表中，参见第 7.1.1 节以更改此行为。ORDER= 选项在第 8.1.5 节中结合 TABULATE 过程进行了讨论。

**2.6.2 理解 ORDER= order=data**

**MEANS 过程**

分析变量：ht 身高（英寸）

| 症状代码 | N 观测 | N | 均值 |
| --- | --- | --- | --- |
| 02 | 10 | 10 | 66.8000000 |
| 10 | 13 | 13 | 68.5384615 |
| 06 | 11 | 11 | 64.0000000 |
| 04 | 13 | 13 | 68.6923077 |
| 03 | 4 | 4 | 66.5000000 |
| 09 | 2 | 2 | 68.0000000 |
| 05 | 8 | 8 | 67.5000000 |
| 01 | 4 | 4 | 67.5000000 |

## 2.6.3 引号内的引号内的引号

引号用于向解析器标识常量文本。有时，这个带引号的常量文本字符串本身会包含引号。幸运的是，SAS 同时提供单引号和双引号，并且任一种都可以用在另一种内部。但是，如果你需要在内部字符串中调用宏变量，会发生什么？无论内部使用哪种引号类型，宏变量都将位于单引号内，因此很可能不会被解析。

以下三条语句中，每条都在一个带引号的字符串内包含另一个带引号的字符串。并且每条都能成功执行。

REPORT 步骤计算块中的一个 DEFINE 例程：

```sas
    call define(_col_,'style', 'style={flyover="myloc"}');
```

执行 Windows DIR 命令的 X 语句：

```sas
    x 'dir "c:\myloc\*.sas" /o:n /b > c:\myloc\pgmlist.txt';
```

用于重定向 LOG 文件的 DM 语句（见第 14.4.2 节）：

```sas
    dm 'log; file "c:\myloc\logdump1.log"';
```

现在假设我们需要在上述示例中嵌入宏变量。由于宏变量在单引号内使用时不会被解析，我们不仅需要理解这些语句如何被解析和执行，还需要理解如何重新编写它们。

```sas
%let temp = myloc;

call define(_col_,'style', 'style={flyover="&temp"}'); ❶

x 'dir "c:\\&temp\\*.sas" /o:n /b > c:\\&temp\\pgmlist.txt'; ❷

dm 'log; file "c:\\&temp\\logdump1.log"'; ❸
```

简单地将宏变量替换到语句中并不总是有效。有趣的是，它也不一定会失败。

- ❶ 虽然通常情况下，宏变量出现在单引号内时不会被解析，但这并非严格成立。CALL DEFINE 例程仅从 PROC REPORT 计算块（未显示）内部调用，并且由于这些块的执行方式，即使宏变量位于单引号内，它也会被解析。无需做任何特殊处理。

- ❷ X 语句按当前编码方式不会工作；宏变量不会被解析。当我们在 Windows 下向操作系统传递路径时，路径应括在双引号中。在当前版本的 SAS 中，X 语句通常不再需要使用包围要传递给操作系统的命令的引号。

  ```sas
  x dir "c:\\&temp\\*.sas" /o:n /b > c:\\&temp\\pgmlist.txt;
  ```

  这简化了语句并消除了问题。当这不起作用时，可以考虑用于 DM 语句的解决方案之一。

- ❸ 在 DM 语句中，关键字 DM 后面的字符串必须加引号，并且宏变量不会被解析。宏引用函数可以通过暂时屏蔽单引号直到宏变量被解析之后来提供帮助。由于单引号已被

  ```sas
  dm %unquote(%bquote(')log%bquote(;)'file "c:\\&temp\\logdump1.log" %bquote('));
  ```

  屏蔽，用于分隔两个 DM 命令的分号也必须暂时屏蔽。在执行之前，使用 %UNQUOTE 函数移除宏引用。在 FILENAME 语句中可能也需要类似的方法。这里我们使用管道引擎将 DOS 命令的结果路由到一个虚拟（管道）文件。

  ```sas
  filename list pipe %unquote(%bquote(')dir "&temp\\*.rtf" /o:n /b %bquote('));
  ```

事实上，由于我们延迟了对引号的识别，我们甚至不需要同时使用两种引号。在此处显示的 X 语句中，%STR 函数用于延迟识别内部的一对双引号，直到外部的一对双引号被使用之后。

```sas
x "%str(dm %"&temp\\output&"; )";
```

在 SAS 中，通过将字符加倍来延迟解析器对字符的识别并不太罕见。在语言中引入双引号之前，这种技术很常见。要在标题语句中显示撇号，曾使用两个单引号。这之所以有效，是因为解析器看到两个单引号，并在第二次识别时将其解释为单个撇号。

```sas
title1 'Tom''s Truck';
```
