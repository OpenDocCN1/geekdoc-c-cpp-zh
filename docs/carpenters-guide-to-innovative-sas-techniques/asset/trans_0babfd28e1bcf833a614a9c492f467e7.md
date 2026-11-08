

> NOTE: 丢失卡片。
> sex=M fname=Adam lname=_ERROR_=1 _N_=6
> NOTE: 从 infile PATLIST 读取了 12 条记录。
>       最小记录长度为 13。
>       最大记录长度为 26。
> NOTE: 当 INPUT 语句越过行尾时，SAS 转到了新的一行。

生成的数据集存在若干数据问题。即使快速检查数据也会发现，数据字段已经发生混淆。

### 1.3.4a 变长记录

| 观测 | 性别 | 名 | 姓 |
|---:|:---:|:---|:---|
| 1 | F | Linda | M Ronald |
| 2 | F | M Mat | M David |
| 3 | F | Merrie | F June |
| 4 | M | Mery | M Matthew |
| 5 | M | Robert | M Arthur |

我们的 INPUT 语句请求 SAS 从第 18 列开始读取 15 个字符位置；然而，从来不会有 15 列可用（最长的记录是最后一条——Robertson——其姓为 9 个字符）。为满足我们的请求，它会跳到下一条物理记录的第 1 列来读取姓。发生这种情况时，就会生成 LOG 中提到的那些 NOTE 消息。

## INFILE 语句选项（TRUNCOVER、MISSOVER）

有两个 INFILE 语句选项在控制 SAS 如何处理*短*记录时特别有用。

- **MISSOVER** —— 为物理记录末尾之外的变量分配缺失值。部分变量会被设为缺失。
- **TRUNCOVER** —— 为物理记录末尾之外的变量分配缺失值。部分变量会被截断，但不一定设为缺失。
- **FLOWOVER** —— SAS 使用下一条物理记录来完成逻辑记录。这是默认行为。

```
title '1.3.4b Varying Length Records';
title2 'Using TRUNCOVER';
data patients(keep=sex fname lname);
    infile patlist truncover;
    input @2  sex $1.
          @8  fname $10.
          @18 lname $15.;
run;
```

指定了 TRUNCOVER 选项，并且会从每条记录中收集尽可能多的信息；但是，SAS 不会转到下一条物理记录来完成观测。

### 1.3.4b 变长记录
使用 TRUNCOVER

| 观测 | 性别 | 名 | 姓 |
|---:|:---:|:---|:---|
| 1 | F | Linda | Maxwell |
| 2 | M | Ronald | Mercy |
| 3 | F | Rachel |  |
| 4 | M | Mat | Most |
| 5 | M | David | Nabers |
| 6 | F | Terrie | Nolan |
| 7 | F | June | Olsen |
| 8 | M | Merv | Panda |
| 9 | M | Mathew | Perez |
| 10 | M | Robert | Pope |
| 11 | M | Arthur | Reilly |
| 12 | M | Adam | Robertson |

通常，TRUNCOVER 选项比 $VARYING 信息格式更易于应用，而且即使你认为自己不需要它，在 INFILE 语句中包含 TRUNCOVER 选项也没有坏处。

通过在 INFILE 语句中包含 TRUNCOVER 选项，我们现在已经正确地读取了数据，没有跳过记录，同时为 Rachel 的姓正确分配了缺失值。

## 使用 $VARYING 信息格式

$VARYING 信息格式是为处理可变长度记录而创建的。该信息格式允许我们确定记录长度，然后使用该长度计算要读取多少列。通常，在尝试使用 $VARYING 信息格式之前，应首先尝试在 INFILE 语句上使用更灵活且更易于应用的 TRUNCOVER 选项。

与其他信息格式不同，$VARYING 使用一个辅助值来确定要读取多少字节。该值通常取决于记录的总长度。可以通过 LENGTH= 选项 ❶ 获取记录长度，并使用总记录长度的一部分来读取宽度可变的字段。

下面的示例展示了 $VARYING 信息格式的经典用法，其中记录上的最后一个字段在各条记录之间宽度不一致。这也是 TRUNCOVER 选项所针对的一类数据读取场景。

```
title2 'Using the $VARYING Informat';
data patients(keep=sex fname lname);
    infile patlist lrecl=10; ❶
    input @; ❷
    namewidth = len - 17; ❸
    input @2 sex $1.
          @8 fname $10.
          @18 lname $varying15. namewidth ❹;
run;
```

- ❶ INFILE 语句上的 LENGTH= 选项指定一个临时变量（LEN），用于保存当前记录的长度。
- ❷ 仅带有尾随 @ 的 INPUT 语句用于将记录加载到输入缓冲区。此时会确定长度并将其加载到变量 LEN 中。尾随 @ 会保持该记录，以便可以再次读取它。

### 1.3.4c 变长记录
使用 $VARYING 信息格式

| 观测 | 性别 | 名 | 姓 |
|---:|:---:|:---|:---|
| 1 | F | Linda | Maxwell |
| 2 | M | Ronald | Mercy |
| 3 | F | M | Mat ❺ |
| 4 | M | David | Nabers |
| 5 | F | Terrie | Nolan |
| 6 | F | June | Olsen |
| 7 | M | Merv | Panda |
| 8 | M | Mathew | Perez |
| 9 | M | Robert | Pope |
| 10 | M | Arthur | Reilly |
| 11 | M | Adam | Robertson |

- ❸ 计算姓的宽度（总长度减去姓名左侧的字符数）。变量 NAMEWIDTH 保存该值，供 $VARYING 信息格式使用。

对于这条特定记录，姓字段的宽度遵循 `$VARYING15.` 信息格式。这里，与 `$VARYING` 信息格式一起使用的宽度是 `LNAME` 可能的最大宽度，同时也确定了该变量的长度。

检查生成的数据可以看出，我们现在读取到了正确的姓；但是，第三行和第四行输入数据仍然存在数据问题。由于第三行数据没有姓，`$VARYING` 信息格式会跳到下一条数据记录。上文讨论的 `INFILE` 语句上的 `TRUNCOVER` 选项成功解决了该问题。

事实上，对于第三条记录，使用 `$10.` 信息格式的变量 `FNAME` 会越过记录末尾，从而导致数据被误读。

```
data patients(keep=sex fname lname namewidth);
    length sex $1 fname $10 lname $15;
    infile patients length=len;
    input @;
    if len lt 8 then do;
        input @2 sex $;
    end;
    else if len le 17 then do;
        namewidth = len-7;
        input @2 sex $
              @8 fname $varying. namewidth;
    end;
    else do;
        namewidth = len-17;
        input @2 sex $
              @8 fname $
              @18 lname $varying. namewidth;
    end;
    run;
```

使用 `LENGTH` 语句声明变量长度，可以避免在信息格式中添加宽度。

名和姓都不包括在内。此代码假定性别（SEX）始终存在。

记录太短，无法包含姓，但必须包含至少一个字母的名。

姓必须至少包含一个字母。

变量 `NAMEWIDTH` 将包含最右侧变量的宽度。该变量的值通常并不重要，但这里保留它，以便你可以看到其值随每个观测而变化。

很容易看出，`$VARYING` 信息格式比 `TRUNCOVER` 或 `MISSOVER` 选项更难使用。不过，`$VARYING` 信息格式仍然可能有帮助。在下面由 John King 建议的简化示例中，没有分隔符，但各列宽度并不固定。更有意思的是，宽度不一致的变量并不在输入字符串的末尾。

```
data datacodes;
    length dataname $15;
    input @1 width 2.
          dataname $varying. width
          datacode :2.;
    datalines;
5 Demog43
2 AE65
13lab_chemistry32
    run;
```

第一个字段（WIDTH）包含第二个字段（DATANAME）中的字符数。该值与 $VARYING 信息格式一起使用，以便正确读取数据集名称，同时不会越过名称而读入下一个字段（DATACODE）。

## 另见

Cates（2001）讨论了 MISSOVER 与 TRUNCOVER 之间的差异。关于这些选项的良好比较也可在 SAS 文档中找到：http://support.sas.com/documentation/cdl/en/basics/58133/HTML/default/viewer.htm#a002645812.htm。

SAS 技术支持示例 #37763 使用 $VARYING. 信息格式在 REPORT 示例中写入零长度字符串：http://support.sas.com/kb/37/763.html。

## 1.4 写入分隔文件

大多数现代数据库系统利用元数据使数据本身更有用。例如，在向 Excel 传输数据或从 Excel 传输数据时，SAS 可以利用这种元数据。平面文件不具备元数据的优势，因此必须通过程序本身传递更多信息。出于这个原因，在从一个数据库系统向另一个数据库系统传输信息时，分隔数据文件不应成为我们的首选。话虽如此，我们并不总是有这种选择。我们在第 1.3 节中看到了多种读取分隔数据的技术。

由于 SAS 已经了解给定 SAS 数据集的所有信息（它可以访问元数据），因此写入分隔文件要直接得多。

## 更多信息

关于读取分隔数据的许多讨论也适用于写入分隔数据（见第 1.3 节）。

### 1.4.1 使用带 DLM= 选项的 DATA 步

使用 DATA 步读取分隔数据时，INFILE 语句用于指定若干控制选项。写入分隔文件的过程类似；不过使用的是 FILE 语句。INFILE 语句上出现的许多相同选项也可以在 FILE 语句上使用。这些选项包括：

- DLM=
- DLMSTR=
- DSD

虽然 DSD 选项默认意味着使用逗号作为分隔符，但这两个选项的用法之间存在差异。DSD 选项会使包含内嵌分隔符字符的值被双引号括起来。DSD 选项还会使缺失值显示为两个连续的分隔符，而单独使用 DLM= 时，缺失值会写为句点或空白。

