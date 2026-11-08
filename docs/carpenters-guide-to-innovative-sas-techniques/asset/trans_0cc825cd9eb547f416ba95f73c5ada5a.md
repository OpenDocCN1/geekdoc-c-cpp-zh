

| 观测 | dsn | errvar | errval | errtxt | errrating | SUBJECT | VISIT | LABDT |
|---:|---|---|---:|---|---:|---:|---:|---|
| 1 | advprt.lab_chemistry | potassium | 6.8 | 高值（>6.7） | 2 | 203 | 4 | 09/29/2006 |
| 2 | advprt.lab_chemistry | potassium | 3 | 低值（<3.1） | 1 | 208 | 10 | 03/09/2007 |

从编码角度看，这种方法的美妙之处在于可以根据需要设置任意数量的检查，而每项检查只需再添加一个 DO 块即可实现。对于大型研究和复杂数据表，其缺点就会显现出来。程序虽然不算极其复杂，但可能变得很大。更重要的是，由于每项检查都实现在程序中，新增或修改标准时就需要重新验证程序本身。这些问题可以通过将检验标准存储在程序之外来解决。一种非常方便的方法是将异常标准存储在数据表中（见 2.3.3 节）。

### 更多信息

非数值会在 3.6.1 节中被检测并写入错误数据集。

### 2.3.3 使用宏控制异常报告

在示例 2.3.2b 所示的 DATA 步中，会为每项数据检查构造一个 DO 块。由于这些 DO 块彼此非常相似，它们非常适合由宏语言为我们编写。下面的宏 %ERRRPT 将构建这个 DO 块。

```sas
%macro errrpt(dsn=,errvar=,errval=,errtxt=,errrating=);
    dsn = "&dsn";
    errvar = "&errvar";
    errval = &errval;
    errtxt = "&errtxt";
    errrating= &errrating;
    output errpt;
    end;
%mend errrpt;
```

当在 DATA 步中调用 %ERRRPT 宏时，IF THEN/DO 语句变成：

```sas
if potassium lt 3.1 then do;
    %errrpt(dsn = advprt.lab_chemistry,
           errvar = potassium,
           errval = potassium,
           errtxt = %str(Low value(<3.1%)),
           errrating= 1)

if potassium gt 6.7 then do;
    %errrpt(dsn = advprt.lab_chemistry,
           errvar = potassium,
           errval = potassium,
           errtxt = %str(High value(>6.7%)),
           errrating= 2)

run;
```

尽管我们稍微简化了代码，但在编码工作量上仍未实现大幅节省。当然，我们可以让宏语言承担更多工作。如果我们能告诉宏语言需要哪些检查以及需要多少项检查，那么包括 IF THEN/DO 在内的每个单独宏调用都可以由一次宏调用生成。

存储并传递所需信息的一种简便方法是使用 SAS 数据集。我们可以创建一个数据集，其中包含每项数据异常检查的约束条件。然后，每条观测都可以用来构建数据异常和错误捕获报告。对于前面的示例，该数据集可能包含以下内容。

**2.3.3b 带异常标准的数据集**

| 观测 | errtst | errvar | errval | errtxt | errrating |
|---|---|---|---|---|---|
| 1 | lt 3.1 | potassium | potassium | 低值（<3.1） | 1 |
| 2 | gt 6.7 | potassium | potassium | 高值（>6.7） | 2 |

然后，一个宏会使用该数据集来构建一系列宏变量列表。随后处理这些列表（数据集中的每条观测都会成为一个检验或 DO 块）。下面所示的 %ERRRPT 宏使用一个 SQL 步构建这些列表，然后使用列表中的宏变量创建一系列 DO 块，以“填空”。

```sas
%macro errrpt(dsn=, bylist=subject); ❶
%local i chknt;
proc sql noprint;
    select errtst, errvar, errval, errtxt, errrating
        into :errtst1-:errtst99, ❷
        :errvar1-:errvar99,
        :errval1-:errval99,
        :errtxt1-:errtxt99,
        :errrating1-:errrating99
        from vallab; ❸
    %let chknt = &sqlobs; ❹
    quit;
data errrpt(keep=dsn errvar errval errtxt errrating &bylist); ❺
    length dsn     $25
           errvar  $15
           errval  $25
           errtxt $15
           errrating 8;
    set &dsn ❻ ;
%do i = 1 %to &chknt; ❼
    %* Write as many error checks as are needed;
    if &&errvar&i &&errtst&i ❽ then do;
        dsn = "&dsn";
        errvar = "&&errvar&i"; ❾
        errval = &&errval&i;
        errtxt = "&&errtxt&i";
        errrating= &&errrating&i;
        output errrpt;
        end;
%end;
run;
%mend errrpt;
%errrpt(dsn=advrpt.lab_chemistry,
        bylist=subject visit labdt) ❿
```

- ❶ 宏 %ERRRPT 用于控制错误报告过程。宏 %DO 循环必须出现在宏定义内部。
- ❷ 从控制数据集 ❸ 中读取的值会存储在一系列宏变量中。这些宏变量的形式为 &ERRVAL1、&ERRVAL2 等。这段代码最多允许 99 项检验（不能超过）。把这个数字设得太大没有坏处（我喜欢至少多留一个数量级）；不过，如果数字太小，LOG 或其他地方不会给出提示（值只是不会被保存）。
- ❹ 从控制数据集读取的观测数保存在宏变量 &CHKCNT 中。这将是该数据集的总检查数。
- ❺ 构成主键的变量包含在 KEEP= 列表中。
- ❻ 要检查的数据集在 SET 语句中指定。
- ❼ 宏 %DO 循环将按宏变量 &CHKCNT 中包含的数字进行迭代，即对控制数据集中的每条观测迭代一次。每次迭代都会生成一个 DO 块，每个待执行的检验对应一个 DO 块。
- ❽ 对于第二次 %DO 循环迭代，IF 语句变为：

    ```sas
    if potassium gt 6.7 then do;
    ```

- ❾ 各个宏变量通过 &&VAR&i 这种宏变量形式来引用。在宏 %DO 循环的第二轮（&i=2）中，宏变量引用 &&ERRVAR&i 解析为 &ERRVAR2，而后者又解析为 potassium。
- ❿ 宏调用包含要检查的数据集名称及其 BY 变量列表。

### 更多信息

第 13.5 节将进一步讨论使用数据集驱动宏。

## 2.4 规范化——转置数据

大多数（但并非全部）SAS 过程更倾向于对规范化数据进行操作；规范化数据往往“高而窄”，并且通常包含用于标识各行的分类变量。在下面的数据展示中，每条观测有一个 SODIUM 值，分类变量为 SUBJECT 和 VISIT。

**2.4 规范化数据**

**规范形式**

| 观测 | SUBJECT | VISIT | sodium |
| ---: | --- | ---: | ---: |
| 1 | 208 | 1 | 13.7 |
| 2 | 208 | 2 | 14.1 |
| 3 | 208 | 4 | 14.1 |
| 4 | 208 | 5 | 14.1 |
| 5 | 208 | 6 | 13.9 |
| 6 | 208 | 7 | 13.9 |
| 7 | 208 | 8 | 14.0 |
| 8 | 208 | 9 | 14.0 |
| 9 | 208 | 10 | 14.0 |
| 10 | 209 | 1 | 14.0 |

……表中部分内容未显示……

同一数据也可以以非规范形式呈现；非规范形式通常为某个分类变量的每个水平设置一列。在下面的示例中，每位患者有一条观测，每次访视的钠值占一列。

**2.4 规范化数据**

**非规范形式**

| 观测 | Subject | Visit1 | Visit2 | Visit3 | Visit4 | Visit5 | Visit6 | Visit7 | Visit8 | Visit9 | Visit10 | Visit11 | Visit12 | Visit13 | Visit14 | Visit15 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 208 | 13.7 | 14.1 | 14.1 | 14.1 | 13.9 | 13.9 | 14 | 14.0 | . | 14.1 | 14.2 | 14 | 14.1 | 14.1 | 14.1 |
| 2 | 209 | 14.0 | 14.0 | 13.9 | 14.2 | 14.5 | 13.8 | 14 | . | 13.8 | 14 | 14.1 | 14.2 | 14 | 14.1 | 14.1 |

由于我们收到数据时往往无法控制其形式，因此需要能够既把数据从规范形式转换为非规范形式，也能从非规范形式转换为规范形式。这一过程称为数据转置，相关操作通常通过 PROC TRANSPOSE 或在 DATA 步中完成。

PROC TRANSPOSE 是执行转置操作的一种高效而强大的过程。DATA 步可以更灵活；不过，PROC TRANSPOSE 的优点是无需在转置之前知道将有多少个转换后的变量。

### 另请参阅

Toby Dunn（2010）讨论了规范数据形式与非规范数据形式之间的差异，并提出了选择其中一种形式而非另一种形式的编程动机。在转置的同时进行汇总时，MEANS 和 SUMMARY 过程可能非常有用。King 和 Zedb（2010）使用 OUTPUT 语句上的 IDGROUP 选项来控制转置过程。

### 2.4.1 使用 PROC TRANSPOSE

对大多数用户而言，PROC TRANSPOSE 往往不太直观。编码并不特别困难；然而，对大多数用户来说，通常很难想象结果数据集会是什么样子。这个过程中还有一个陷阱，一旦触发，可能会导致数据损坏。

下面的步骤创建实验室化学数据的非规范版本，演示了一个简单的 PROC TRANSPOSE，并且还将用来演示 PROC TRANSPOSE 的陷阱。

```sas
    proc transpose data=lab_chemistry(keep=subject visit sodium) ❶
        out=lab_nonnormal(keep=subject visit:) ❷
        prefix=Visit; ❸
      by subject; ❹
      var sodium; ❺
    run;
```

- **DATA=** 用于指定输入数据集。
- **转置后的数据集**由 **OUT=** 选项命名。请注意，这里使用冒号来选择所有以字母 **VISIT** 开头的变量名（关于变量名快捷方式的更多内容，见 2.6.1 节）。
- **PREFIX=** 选项用于指定将用来构成新列名的文本。

