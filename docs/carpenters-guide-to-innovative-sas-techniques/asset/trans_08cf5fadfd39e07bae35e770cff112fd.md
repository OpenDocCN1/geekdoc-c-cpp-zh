
## 6.1 一系列 IF 语句——逻辑查找

最简单的表格查找形式利用 IF-THEN 语句。尽管易于编码，但这是最慢的表格查找方法之一。本质上，该技术通过 IF-THEN 处理创建带关联值的新变量。实际上，我们是在程序内“硬编码”诊所名称。以下 DATA 步演示了该技术。

```sas
data demogname;
  set advrpt.demog(keep=clinnum lname fname);
  length clinnum $35;
  if clinnum='011234' then clinname = 'Boston National Medical';
  if clinnum='014321' then clinname = 'Vermont Treatment Center';
  if clinnum='107211' then clinname = 'Portland General';
  if clinnum='108531' then clinname = 'Seattle Medical Complex';
  if clinnum='023910' then clinname = 'New York Metro Medical Ctr';
  if clinnum='024477' then clinname = 'New York General Hospital';
  run;
```

这种方法的问题在于，如果要查找的代码超过极少数几个，就不实用；此外，它非常低效。SAS 必须执行每个 IF 语句，即使发现较早的 IF 语句为真。更糟的是，IF 语句需要相当多的处理时间。

这是 100% 查找的示例。它是一种顺序搜索，并且无论是否已经找到答案，都会检查每个代码。

## 6.2 IF-THEN/ELSE 查找语句

比 IF-THEN 快得多的方法是使用 IF-THEN / ELSE 语句组合。以下 DATA 步执行速度比前一个更快，因为一旦发现某个 IF 语句为真，其关联的 ELSE 就不会执行。因此，一旦某个表达式被判断为真，其余 IF-THEN / ELSE 语句都不会执行。如果将更可能的结果放在列表更靠前的位置，该技术可以变得更快一些。

```sas
data demogname;
  set advrpt.demog(keep=clinnum lname fname);
  length clinnum $35;
  if clinnum='011234' then clinname = 'Boston National Medical';
  else if clinnum='014321' then clinname = 'Vermont Treatment Center';
  else if clinnum='107211' then clinname = 'Portland General';
  else if clinnum='108531' then clinname = 'Seattle Medical Complex';
  else if clinnum='023910' then clinname = 'New York Metro Medical Ctr';
  else if clinnum='024477' then clinname = 'New York General Hospital';
  run;
```

就性能效率而言，该技术类似于 DATA 步的 SELECT 语句和 SQL 中的 CASE 语句。在执行表查找时，SELECT 语句与 IF-THEN / ELSE 组合相当。它甚至可以稍快一些（Virgle，1998）。同样，当最可能的匹配位于列表靠前位置时，处理时间会最小化。

```sas
data demogname;
    set advrpt.demog(keep=clinnum lname fname);
    select(clinnum);
       when ('011234') clinname='Boston National Medical';
       when ('014321') clinname='Vermont Treatment Center';
       when ('107211') clinname='Portland General';
       when ('108531') clinname='Seattle Medical Complex';
       when ('023910') clinname='New York Metro Medical Ctr';
       when ('024477') clinname='New York General Hospital';
       otherwise;
    end;
    run;
```

有趣的是，Virgle（1998）发现，有时将整个表达式放在 WHEN 语句上可以增强 SELECT 语句的效率。

```sas
data demogname;
    set advrpt.demog(keep=clinnum lname fname);
    select;
       when(clinnum='011234') clinname='Boston National Medical';
       when(clinnum='014321') clinname='Vermont Treatment Center';
       when(clinnum='107211') clinname='Portland General';
       when(clinnum='108531') clinname='Seattle Medical Complex';
       when(clinnum='023910') clinname='New York Metro Medical Ctr';
       when(clinnum='024477') clinname='New York General Hospital';
       otherwise;
    end;
    run;
```

这些技术有两个首要问题。主要问题是搜索是顺序的。当列表很长时，平均比较次数会迅速增加，即使你仔细排列列表也是如此。第二个但同样重要的问题是，这些技术将值硬编码在程序中。这根本算不上明智的编程。

幸运的是，本章中的其他查找技术不仅完全避免了硬编码，而且最大程度减少了顺序搜索的需求。

## 6.3 DATA 步合并与 SQL 连接

在 SQL 步中使用连接以及在 DATA 步中使用 MERGE，是通过匹配两个数据集之间的值来执行表查找的另一种非常常见的方式。MERGE 语句（通常与 BY 语句一起使用时）要求数据集已排序或建立索引，而 SQL 步则不需要。两种过程各有优缺点。

### MERGE 语句

MERGE 语句用于合并两个或多个数据集。就本讨论而言，其中一个数据集将包含要查找的信息。BY 语句用于确保观测正确对齐。BY 语句

### SQL 连接

使用 SQL 时，合并过程称为 *连接*。SQL 连接操作不需要排序，并且可能比 DATA 步 MERGE 更高效，除非表太大而无法很好地放入内存。

仅仅因为 SQL 连接不要求输入数据已排序，并不意味着在准备连接（查找）时不会消耗任何资源。在 SQL 步处理内部，查找技术正在被应用，只是对用户不可见。这些后台操作与我们可以在 DATA 步中显式应用和控制的哈希技术非常相似（见 6.7 节和 6.8 节）。

SQL 中有多种不同类型的连接，其中一种与上一步密切匹配的连接如下所示。

在本例中，我们添加了要求（通过使用 WHERE 子句 ❷）：诊所编号必须同时存在于两个数据表中。WHERE 子句用于选择两个输入表中 CLINNUM 值匹配的行。这比上面 ❶ 所示 DATA 步中使用的条件更严格。

```sas
proc sql noprint;
   create table demognames2 as
      select a.clinnum, b.clinname, lname, fname
      from advrpt.demog a, advrpt.clinname b
      where a.clinnum=b.clinnum; ❷
   quit;
```

SQL 不要求两个数据集在连接前排序，并且除非我们明确要求结果数据表排序（ORDER BY 子句），否则它将反映输入数据的顺序。这可以从下面 PROC PRINT 结果中诊所编号的顺序看出。

6.3 通过连接或合并两个表进行查找  
连接后数据的 10 个观测

| 观测 | clinnum | clinname | lname | fname |
|---:|---:|---|---|---|
| 1 | 049060 | 亚特兰大综合医院 | 亚当斯 | 玛丽 |
| 2 | 082287 | 丹佛安全医院 | 亚当森 | 琼 |
| 3 | 066789 | 奥斯汀医疗医院 | 亚历山大 | 马克 |
| 4 | 063742 | 休斯敦综合医院 | 安特勒 | 彼得 |
| 5 | 023910 | 纽约大都会医疗中心 | 阿特伍德 | 特迪 |
| 6 | 066789 | 奥斯汀医疗医院 | 班纳 | 约翰 |
| 7 | 046789 | 坦帕治疗中心 | 巴伦 | 罗杰 |
| 8 | 049060 | 亚特兰大综合医院 | 巴特尔 | 玛丽 |
| 9 | 095277 | 旧金山湾区综合医院 | 布洛克 | 威尔 |
| 10 | 031234 | 贝塞斯达先锋医院 | 坎德尔 | 西德 |

*....表中部分内容未显示....*

## 6.4 使用双重 SET 语句进行合并

已有许多已发表的方案在同一 DATA 步中使用两个 SET 语句。这些 SET 语句取代单个 MERGE 语句，由程序员负责连接过程（使两个数据集保持同步）。这些技术可能比 MERGE 更快，但更复杂。然而，它们仍然要求两个输入数据集都已排序。
