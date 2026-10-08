
如果你使用文件引用（`filref`），则不需要 `PRINT` 选项。如果在交互会话中指定 `PRINT`，输出窗口会将换页符解释为分页，并移除换页符之前的空行。将结果写入平面文件会产生没有分页的文件。如果文件需要包含换页符，则 `FILE` 语句应包含 `PRINT` 选项。

## `RECF=`record-format

指定输出的记录格式。

## `STOPOVER`

如果 `PUT` 语句尝试写入超出长度的数据项，立即停止 `DATA` 步。在这种情况下，SAS 会丢弃超出长度的数据项，写入之前构建的部分行，并发出错误消息。

**默认：**`FLOWOVER`

**参见：**第 82 页的 `FLOWOVER` 和第 80 页的 `DROPOVER`

## `TITLES` | `NOTLES`

控制页面上标题行的打印。当省略 `NOTLES` 或指定 `TITLES` 时，SAS 会打印任何当前定义的标题。

**别名：**`TITLES`

**默认：**`TITLES`

## `_FILE=`variable

引用此 `FILE` 语句当前输出区的字符变量。你可以像使用其他变量一样使用该变量，甚至作为赋值的目标。该变量会被自动识别并初始化为空格。与自动变量一样，`_FILE=` 不写入数据集。

**限制：**`variable` 不能是之前定义的变量。确保 `FILE =` 规范是该变量在 `DATA` 步中首次出现。不要使用 `LENGTH` 或 `ATTRIB` 语句设置或更改 `_FILE` 变量的长度。

**交互：**此字符变量的最大长度是指定 `FILE` 语句的记录长度 (`LRECL`)。SAS 在执行阶段之前不会打开文件以获取 `LRECL`。因此，在编译阶段该变量的大小为 32767 字节。

**提示：**对此变量的修改会直接修改 `FILE` 语句的当前输出缓冲区。任何针对 `FILE` 的后续 `PUT` 语句都会输出修改后的缓冲区内容。`_FILE` 变量仅访问当前的

# `FILE` 语句 87

如果使用 `N=` 来指定多个输出缓冲区，则为指定的 `FILE` 语句的输出缓冲区。

若要在另一个语句中使用 `_FILE_ =` 选项访问输出缓冲区的内容，请使用自动变量 `FILE_`。

参见：第 88 页的“更新 `_FILE_` 变量”

## 运行环境选项

有关 `FILE` 语句中特定于运行环境的选项说明，请参考你所运行环境的 SAS 文档。

## 详细

### 概述

默认情况下，`PUT` 语句的输出被写入 SAS 日志。使用 `FILE` 语句可以将此输出路由到与过程输出相同的外部文件，或路由到不同的外部文件。你可以指定是否向文件中添加回车控制符。请参见第 86 页的 `PRINT|NOPRINT` 选项。

你可以在条件（`IF-THEN`）处理处理中使用 `FILE` 语句，因为它是可执行的。你还可以使用多个 `FILE` 语句在单个 `DATA` 步中写入多个外部文件。

## 运行环境信息

使用 `FILE` 语句需要特定于运行环境的信息。在使用此语句之前，请参考你所运行环境的 SAS 文档。

你可以结合 `FILE` 语句使用输出交付系统（ODS）来写入 `DATA` 步结果。详情请参阅《SAS 输出交付：用户指南》中的“用于 ODS 的 `FILE` 语句”。

## 原地更新外部文件

你可以结合 `INFILE` 和 `PUT` 语句使用 `FILE` 语句来原地更新外部文件，更新整个记录或仅记录中的选定字段。请遵循以下指南：

- 始终将 `INFILE` 放在前面。
- 在 `INFILE` 和 `FILE` 语句中指定文件引用（`fileref`）或物理文件名。
- 在 `INFILE` 语句中使用 `INFILE` 和 `FILE` 语句通用的选项。（在 `FILE` 语句中使用的任何选项将被忽略。）
- 在 `INFILE` 语句中使用 `SHAREBUFFERS` 选项允许 `INFILE` 和 `FILE` 语句使用相同的缓冲区，这可以节省 CPU 时间并允许更新更新字段而不是整个记录。

## 访问输出缓冲区的内容

除了 `_FILE=` 变量外，你还可以使用自动 `FILE` 变量来引用 `FILE` 语句最近执行时的当前输出缓冲区的内容。该字符变量会被自动保留并初始化为空格。

当你在 `FILE` 语句中使用 `_FILE=` 选项时，该变量也会被自动 `_FILE_` 变量间接引用。如果自动 `_FILE_` 变量且你在特定的 `FILE` 语句中省略了 `_FILE`，则 SAS

![](img/df01a42b751f4ba4ce8fe6c9da27f93d_100_0.png)

## 更新 `_FILE_` 变量

与其他 SAS 变量一样，你可以更新 `_FILE_` 变量。以下是两种方法：

- 在赋值语句中使用 `_FILE_`。
- 使用 `PUT` 语句。

可以使用如下形式的赋值语句来更新 `_FILE_` 变量。

```
_FILE_ = '引号内的字符串' 字符表达式
```

赋值语句更新当前输出缓冲区的内容，并将缓冲区长度设置为“引号内的字符串”或字符表达式的长度。

然而，使用赋值语句不会影响 `PUT` 语句的当前列指针。该 `FILE` 的下一个 `PUT` 语句将从第 1 列开始更新缓冲区，或者当你在 `PUT` 语句中使用尾随的 `@` 时，从最后一个位置开始更新。

在以下示例中，赋值语句更新了当前输出缓冲区的内容。`PUT` 语句的列指针不受影响：

```
file print;
_file_ = 'FILE';
put 'This is PUT';
```

SAS 创建输出：This is PUT

在此示例中，

```
file print;
_file_ = 'This is from FILE, sir.';
put @14 'both';
```

SAS 创建输出：This is from both, sir.

你也可以通过 `PUT` 语句来更新 `_FILE_` 变量。`PUT` 语句更新 `_FILE_` 变量是因为 `PUT` 语句格式化输出缓冲区中的数据，且 `FILE` 指向该缓冲区。但默认情况下，SAS 在执行 `PUT` 语句后会清除缓冲区并输出记录（或 `N=` 块记录）。

因此，如果你想在输出之前检查或进一步修改 `_FILE_` 的内容，请在任何 `PUT` 语句包含尾随的 `@` 或 `@@`（当 `N=1` 时）。对于其他 `N` 值，在最后行指针为记录块最后一条记录的 `PUT` 语句中使用尾随的 `@` 或 `@@`。在以下示例中，当 `N=1` 时

```
file ABC;
put 'Something';
Y = _file||' is here';
file ABC;
put 'Nothing';
Y = _file_||' is here;
```

`Y` 首先赋值为 Something is here，然后 `Y` 被赋值为 here。

对 `_FILE_` 的任何修改都会直接修改当前 `FILE` 语句的当前输出缓冲区。该 `FILE` 的任何后续 `PUT` 语句的执行将输出修改后缓冲区的内容。

`_FILE_` 只访问 `FILE` 语句当前输出缓冲区的内容，即使你使用 `N=` 选项指定多个缓冲区。你可以访问所有 `N=` 缓冲区，但必须使用带有 `#` 行指针控制的 `PUT` 语句产生所需的当前输出缓冲区。

## 比较

- `FILE` 语句指定 `PUT` 语句的输出文件。`INFILE` 语句指定 `INPUT` 语句的输入文件。
- `FILE` 和 `INFILE` 语句都允许你使用选项为 SAS 提供有关文件的额外信息。

## 示例

#### 示例 1：在开始页面时执行语句

此 `DATA` 步说明了如何使用 `HEADER=`：

- 编写报告。使用 `DATA_NULL` 编写报告而不是创建数据集。

```
data_null;
file print;
```

- 开启新页。`PRINT` 是文件引用。SAS 使用回车控制符以打印文件的特性写入输出。

```
if first.dept then put_page;
@20 sales;
```

- 为每页编写页眉：newpage；

```
put 'Sales for 1989' /
@20 dept=
return;
```

#### 示例 2：根据当前页剩余行数确定新页

此 `DATA` 步演示了使用 `LINESLEFT` 来确定分页位置。

- 编写报告。使用 `DATA_NULL` 编写报告而不是创建数据集。

```
data_null;
set info;
```

- 路由到标准输出窗口。`PRINT` 文件引用路由到与输出相同的位置。`LINESLEFT` 表示变量保持为剩余的行数：

```
file print linesleft=remain pagesize=20;
@5 name @30 phone
```

- 当当前页剩余少于七行时开始新页。在此条件下，`PUT_PAGE` 会在 line 行处开始一个新页：

#### 示例 3：安排整个页的内容

此示例展示了如何在 `DATA` 步中使用 `N=PAGESIZE` 来生成双列电话簿列表，每列包含姓名和电话号码：

- 创建报告并将其写入 SAS 输出窗口。使用 `DATA_NULL` 编写报告而不是创建数据集。`PRINT` 是文件引用。SAS 使用回车控制符以打印文件的特性写入输出。`N=PAGESIZE` 使输出指针可以使用页面：

```
data_null;
file 'external-file' print pagesize;
```

- 指定报告的列。此 `DO` 循环在每次 `DATA` 步迭代中迭代两次。`COL` 值在第一次迭代为 1，在第二次迭代为 40：

```
dol=col=1;
```

- 写入 20 行数据。此 `DO` 循环迭代 20 次在第一列写入 20 行。完成后，外部循环将 `COL` 设置为 40，此 `DO` 循环迭代 20 次，在第二列写入 20 行数据。`LINE` 和 `COL` 的值由 `DO` 语句增加，控制 `PUT` 语句在页面写入 `NAME` 和 `PHONE` 值的位置：

```
dol=1 to 20;
set info;
put #line @col name @20. +1 phone 4;
end;
```

- 在组合两列数据后，写入页面。此 `END` 语句结束外部 `DO` 循环。`PUT_PAGE` 当前页面并将指针移动到新页顶部：

```
end;
put_page;
run;
```

# 示例 4：识别当前输出文件

此 `DATA` 步会在日志中打印一条文件识别消息，并将当前输出文件的值分配给变量 `MYOUT`。`PUT` 语句演示了如何为 `MYOUT` 分配正确的值，并会将该变量的值写入输出文件：

```
data_null_
length myout $ 200;
file-specification filename=myout;
put myout=
stop;
run;
```

`PUT` 语句向当前输出文件写入一行，其内容包含该文件的物理名称：

```
MYOUT=your-output-file
```

# 示例 5：动态更改当前输出文件

此 `DATA` 步使用 `FILEVAR=` 选项将当前打开的输出文件动态更改为新的物理文件。

- 编写报告。创建一个长字符变量。使用 `DATA_NULL_` 写报告而不是创建数据集。`LENGTH` 语句创建一个长度足够以容纳外部文件名名的变量：

```
data_null_
length name $ 200;
```

- 读取一行流式数据并为 `NAME` 变量赋值：

`input name $;`

- 当 `NAME` 变量发生变化时，关闭当前输出文件并打开新文件。文件规范只是占位符；可以是任何有效的 SAS 名称：

`file-specification filevar=name mod;date=date();`

- 向当前打开的输出文件追加一条日志记录：

`put 'records updated ' date date;`

- 提供外部文件的名称：

```
datalines;
external-file-1
external-file-2
external-file-3
;
```

# 示例 6：当输出行超过输出文件的行长度时

由于变量的组合长度超过了输出行（80 个字符），此 `PUT` 语句写入了三条独立的记录：

```
file-specification linesize=80;
put name $ 1-50 city $ 71-90 state $ 91-104;
```

`NAME` 的值出现在第一条记录中，`CITY` 从第二条记录的第一列开始，`STATE` 从第三条记录的第一列开始。

## 示例 7：通过 TCP/IP Socket 读取数据并写入文本

此示例展示了如何通过 TCP/IP Socket 从文件读取原始数据。

`INFILE` 语句中使用了 `NBYTE=`

```
* 首先作为服务器启动此 */
filename serve socket ':5205' server
recfm=s
lrecl=25 blocksize=2500;
data_null;
nb=25;
infile serve nbyte=nb;
input text $char25;
put all_;
run;
```

此示例展示了如何通过 TCP/IP Socket 向文件写入文本：

```
* 当服务器文本运行时.*/
/* 以客户端身份继续执行此操作。 */
filename client socket '&hostname:5205'
recfm=s
lrecl=25 blocksize=2500;
data_null;
file client;
put 'Some text to length 25...';
run;
```

# 示例 8：在写入输出文件时指定编码

此示例从 SAS 数据集创建一个外部文件。当前会话的编码为 Latin1；外部文件的编码需要为 UTF-8。SAS 使用当前会话编码写入外部文件。

要告诉 SAS 在向外部文件写入数据时使用何种编码，请指定 `ENCODING=` 选项。当告诉 SAS 外部文件为 UTF-8 编码时，SAS 在写入外部文件时会将数据从 Latin1 转码为指定的 UTF-8 编码。

```
libname myfiles 'SAS-library';
filename output 'external-file';
data_null;
 myfiles.cars;
file output encoding="utf-8";
put Make Model Year;
run;
```

# 示例 9：使用 FTP 访问方法将数据写入 Excel 表格

此示例使用 FTP 访问方法和 `FILEVAR` 选项将数据写入多个 Microsoft 工作表。

```
data_null;
 i = 1 to 3;
 sheet = 'excel[test-sheet.xlsx]Sheet', i, '!r1c1:r10c2';
 area ftp filevar=;
 x = 1 to 10;
 y = 2*x;
 put x y;
 end;
end;
```

```
run;
```

# 查看《SAS Language Reference: Concepts》第 3 章中的“当我按字节测量 SAS 名称长度时，可以使用多少字符？”

- 语句：

第 93 页的“`FILENAME Statement`”

第 165 页的“`INFILE Statement`”

第 222 页的“`LABEL Statement`”

第 288 页的“`PUT Statement`”

第 333 页的“`RETURN Statement`”

第 360 页的“`TITLE Statement`”

《SAS Output Delivery System: User's Guide》中的“`FILE Statement for ODS`”

# `FILENAME` 语句

将 SAS 文件引用与外部文件或输出设备关联，解除文件引用与外部文件的关联，或列出外部文件。

| 有效于： | 任意 |
| :--- | :--- |
| 类别： | 数据访问 |
| 查看： | Windows、UNIX 和 z/OS 下的 `FILENAME Statement` |

## 语法

```
Form 1: FILENAME fileref <device-type> 'external-file' <encoding=encoding-value> <options> <operating-environment-options>
Form 2: FILENAME fileref <device-type> <options> <operating-environment-options>
Form 3: FILENAME fileref <device-type> | <options> | <operating-environment-options>
Form 4: FILENAME fileref <device-type> | <options>;
```

## 参数

`fileref`

与外部文件或输出设备关联的 SAS 文件引用，解除文件引用与外部文件的关联，或列出外部文件。

`<device-type>`

设备类型。

`'external-file'`

外部文件。

`<encoding=encoding-value>`

编码=编码值。

`<options>`

选项。

`<operating-environment-options>`

操作系统选项。

## 示例

`PUT` 语句向当前输出文件写入一行，其内容包含该文件的物理名称：

```
MYOUT=your-output-file
```

...

文件规范只是一个占位符；它可以是任何有效的 SAS 名称：

` `VAR` 变化：

`file-specification filevar=name mod;date=date();`

...向当前打开的输出文件追加一条日志记录：

提供外部文件的名称：

```
datalines;
external-file-1
external-file-2
external-file-3
;
```

# 示例 6：当输出行超过输出文件的行长度时

由于变量的组合长度超过了输出行（80 个字符），此 `PUT` 语句写入了三条独立的记录：

```
file-specification linesize=80;
put name $ 1-50 city $ 71-90 state $ 91-104;
```

`NAME` 的值出现在第一条记录中，`CITY` 从第二条记录的第一列开始，`STATE` 从第三条记录的第一列开始。
