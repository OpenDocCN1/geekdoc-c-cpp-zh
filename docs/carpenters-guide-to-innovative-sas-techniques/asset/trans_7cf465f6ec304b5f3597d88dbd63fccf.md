
## 5.2 在 PDV 上重排变量

**CONTENTS 过程**

**按创建顺序排列的变量**

| # | 变量 | 类型 | 长度 | 格式 | 标签 |
|---:|---|---|---:|---|---|
| 1 | subject | Num | 8 |  |  |
| 2 | clinnum | Char | 6 |  | 诊所编号 |
| 3 | lname | Char | 10 |  | 姓 |
| 4 | fname | Char | 6 |  | 名 |
| 5 | ssn | Char | 9 |  | 社会安全号码 |
| 6 | sex | Char | 1 |  | 患者性别 |
| 7 | dob | Num | 8 | DATE7. | 出生日期 |
| 8 | death | Num | 8 | DATE7. | 死亡日期 |
| 9 | race | Char | 1 |  | 种族 |
| 10 | edu | Num | 8 |  | 受教育年数 |
| 11 | wt | Num | 8 |  | 体重（磅） |
| 12 | ht | Num | 8 |  | 身高（英寸） |
| 13 | symp | Char | 2 |  | 症状代码 |
| 14 | death2 | Num | 8 | DATE9. |  |

在下面的示例中，只有 ADVRPT.DEMOG 中的少数变量会流入新数据集，并且通过使用 LENGTH 语句改变了这些变量的顺序。

```sas
data demog2(keep=subject lname fname sex ht wt dob symp);
   length lname $10 fname $6 sex $1 symp $2;
   set advrpt.demog(keep=subject lname fname sex edu
                    death ht wt dob symp);
   where death and edu>15;
run;
```

❶ KEEP 和 DROP 语句/选项不会改变或影响 PDV 上变量的顺序。

❷ LENGTH 语句不仅用于为这四个变量指定长度属性，还会将它们添加到 PDV。由于 LENGTH 语句出现在 SET 语句之前，因此这些变量及其关联属性会在 SET 语句贡献任何变量或属性之前被添加到 PDV。对于这些变量中尚未指定的属性（例如格式或标签），将从 SET 语句中指定的输入数据集的元数据中获取。

❸ 尽管变量 DEATH 和 EDU 不会包含在新数据集中，但它们必须存在于 PDV 上，以供 WHERE 语句使用。

| Obs | lname | fname | sex | symp | subject | dob | wt | ht |
|---:|---|---|---|---:|---:|---|---:|---:|
| 1 | James | Debra | F | 05 | 232 | 19JUN42 | 163 | 63 |
| 2 | Manley | Debra | F | 05 | 241 | 19JAN42 | 163 | 63 |

请注意，虽然 LENGTH 语句中的变量顺序发生了变化，但其余变量的顺序与输入数据中的顺序相同。

ARRAY、FORMAT、INFORMAT、RETAIN 和 ATTRIB 语句也可以以类似方式用于在 PDV 上重排变量。KEEP、DROP 和 RENAME 语句不能用于改变变量顺序。通常，重排变量时推荐选择 RETAIN 语句，因为它不需要任何其他属性，也不会以其他方式改变通过 SET 或 MERGE 语句引入 DATA 步的变量的行为。

在前面的示例中，LENGTH 语句 ❷ 本可以替换为 RETAIN 语句，后者不需要额外了解待重排变量的属性。

```sas
retain lname fname sex symp;
```

也可以使用 SQL 步重排变量。这里使用 SELECT 语句 ❶ 指定新的变量顺序。请注意，与 DATA 步不同，必须指定完整的变量列表，除非使用星号（*）❷ 指定所有变量；在这种情况下，你将看到它们按 PDV 顺序排列。

```sas
proc sql ;
create table demog4 as
❶ select lname, fname, sex, symp, subject, dob, wt, ht
  from advrpt.demog(keep=subject lname fname sex
  edu death ht wt dob symp)
  where death and edu>15;
  select * ❷
  from demog4;
quit;
```

在一个步骤中读取多个数据集时，变量顺序在一定程度上由数据集的读取顺序决定。变量按编译器遇到它们的顺序添加到 PDV。从编译器看到的第一个数据集中取得的变量将首先写入 PDV。尚未出现在 PDV 上的变量将按它们在后续数据集中被遇到的顺序添加到 PDV。这意味着，你可以通过控制输入数据集首次出现的顺序，在一定程度上控制变量顺序。

### 更多信息

尽管我并不一定推荐使用这些缩写，但某些变量列表缩写要求你具体了解变量的顺序（参见第 2.6.1 节）。

### 另请参阅

SAS 使用说明 8395 在 http://support.sas.com/kb/8/395.html 讨论了变量重排。

## 5.3 创建和维护索引

令人有点惊讶的是，实际利用索引的程序员少之又少。诚然，这个话题可能有点复杂；毕竟，已经有一本书专门讨论这个主题（Raithel, 2006）。无论复杂与否，你都不需要大量知识就能利用它们。

索引让我们能够对数据表进行虚拟排序，而无需实际排序。可以为任何给定数据表创建多个索引，并且借助多个索引，可以同时以多种方式有效排序数据集。创建索引后，它允许使用 BY 语句和其他处理技术，就像数据已使用 PROC SORT 排序过一样。索引在取子集和合并场景中也非常有帮助。

### 5.3.1 索引表的元数据

| CONTENTS 过程 | |
|---|---|
| 数据集名称 | ADVRPT.DEMOG |
| 成员类型 | DATA |
| 引擎 | V9 |
| 创建时间 | Tue, Sep 22, 2009 10:57:37 AM |
| 观测数 | 77 |
| 变量数 | 14 |
| 索引数 | 3 ① |
| 观测长度 | 96 |

**索引和属性的字母顺序列表**

| # | 索引 | 唯一值数 | 变量 |
|---:|---|---:|---|
| 1 | group | 23 | sex race edu |
| 2 | ssn | 76 |  |
| 3 | subject | 77 |  |

索引定义也包含在数据集的元数据中，查看 PROC CONTENTS 生成的列表即可看到。每个索引的名称显示在标有 Index ② 的列下。对于复合索引，变量列表也显示在标有 Variables ③ 的列下。

当选择了一个索引时，其使用情况将在 LOG 中提及。

```text
66  proc print data=advrpt.demog;
67      by sex race edu;
NOTE: An index was selected to execute the BY statement.
      The observations will be returned in index order rather than
      in physical order. The selected index is for the variable(s):

sex
race
edu
```

索引实际上并不存储在数据集本身中。相反，它们驻留在一个单独的文件中。在 Windows 下，索引文件与其关联的数据集具有相同的名称；但是，扩展名不同。

### 5.3.2 创建简单索引

可以使用 DATASETS 步、SQL 步或 DATA 步创建索引。接下来的三个步骤各创建一个简单索引。在本节后面，这些索引将用于多个 PROC PRINT 步中。

```sas
proc datasets lib=advrpt;
  modify demog;
  index create clinnum; ② ③
quit;
```

- ❶ 指定接收索引的数据集。该数据集可以是永久数据集或临时数据集。
- ❷ 指定要创建的索引。对于简单索引，其名称与用于构成该索引的单个变量相同。
- ❸ 指定用于定义索引的变量（在 SQL 步中单独指定）。

```sas
proc sql noprint;
  create index clinnum ②
    on advrpt.demog ❶ (clinnum) ③;
quit;
```

```sas
data demog2 ❶(index=(clinnum ②③));
  set advrpt.demog;
run;
```

这三种创建索引的方法的效率往往会因具体数据而异。每种创建索引的方法读取和处理数据的方式都不同。

在这三种创建索引的方法中，DATA 步是唯一读取整个数据集的方法。PROC SQL 和 PROC DATASETS 不会以相同方式读取数据；它们主要只是添加索引文件。这意味着使用 DATA 步生成索引的成本可能更高，并且其成本会随着数据量的增长而增长。

当 MSGLEVEL 系统选项设置为 I ❶ 时，使用索引时会向 LOG 写入一条说明。在这个 PROC PRINT 步中，使用 SSN 变量对数据取子集。LOG 显示已选择 SSN 的索引用于 WHERE 子句。

```sas
* Create index on ssn;
proc sql noprint;
   create index ssn
      on advrpt.demog (ssn);
   quit;

options msglevel=i; ❶

* Use the ssn index;
proc print data=advrpt.demog;
   var lname fname;
   where ssn < '3';
   id ssn;
run;
```

```text
139  proc print data=advrpt.demog;
140     var lname fname;
141     where ssn < '3';
INFO: Index ssn selected for WHERE
clause optimization. ❶
```

创建索引后，使用已索引变量的 BY 语句将导致使用该索引。在两个 PROC PRINT 步中，对同一输入数据集使用了两个不同的 BY ❷ 语句。由于这两个变量都有索引，该数据可能并未按两个 BY 变量中的任何一个排序；但是，两个步骤都将成功执行。

```sas
proc print data=advrpt.demog;
   by clinnum; ❷
   id clinnum;
run;

proc print data=advrpt.demog;
   by ssn; ❸
   id ssn;
run;
```

可以通过使用 PROC DATASETS 从数据集中删除索引。要删除的索引通过其在 INDEX 语句上的名称（简单索引或复合索引）以及 DELETE 选项来标识。在此步骤中，简单索引 CLINNUM 正从 ADVRPT.DEMOG 数据集中删除。

```sas
proc datasets lib=advrpt;
   modify demog;
   index delete clinnum;
   quit;
```
