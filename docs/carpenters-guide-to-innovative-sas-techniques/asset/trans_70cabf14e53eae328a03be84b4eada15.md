
由于 VNEXT 例程可用于检索变量属性，因此随后可以在 DATA 步执行期间使用这些属性来检索数据本身。在以下示例中，字符变量已存储为代码，并且其关联格式已添加到数据集的元数据中。我们需要创建一个具有相同变量名的新数据集，但我们希望值是格式化后的值，而不是存储为代码。在引出问题中，我们不知道要转换多少个变量，甚至不知道它们的名称。Rosenbloom（2011a）使用宏语言解决方案解决了类似问题。

人口统计学数据集（ADVRPT.DEMOG）中的变量 SEX、SYMP 和 RACE 将使用其关联格式重新编码，这些格式在部分展示于此的示例程序中已定义并添加到元数据中。在下面展示的程序中，我们模拟不知道编码变量（SEX、SYMP 和 RACE）的名称。

## 3.6.5 使用变量信息函数

### 检索和使用格式

| Obs | lname | fname | sex | symp | race |
|---:|---|---|---|---|---:|
| 1 | Adams | Mary | F | 02 | 2 |
| 2 | Adamson | Joan | F | 10 | 2 |
| 3 | Alexander | Mark | M | 1 | 1 |
| 4 | Antler | Peter | M | 10 | 2 |
| … | … | … | … | … | … |

……列表的部分内容未显示……

这些变量中的每一个都使用以下 FORMAT 语句分配了格式。请注意，格式的名称不一定与其变量名相同。

```sas
proc sort data=advrpt.demog
    (keep=lname fname sex symp race)
    out=codedat;
  by lname fname; ❶
  format sex $gender. symp $symptom. race $race.;
run;
data namelist(keep=lname fname varname varvalue); ❷
  set codedat;
  length varname $15 varvalue $30; ❸
  array vlist{25} $15 _temporary_; ❹
  if _n_=1 then do until (name=' '); ❺
    call vnext(name,type); ❻
    if upcase(name) not in: ('LNAME' 'FNAME' ❼
                             'NAME' 'TYPE'
                             'VARNAME' 'VARVALUE')
       and type='C' then do;
      cnt+1;
      vlist{cnt}=vnamex(name); ❽
    end;
  end;
  do i = 1 to cnt;
    varname = vlist{i}; ❾
    varvalue = vvaluex(varname);
    output namelist;
  end;
run;
```

- 1. ❶ 使用我们已知名称的关键变量对数据进行排序。当我们将数据转置回其原始形式时，排序顺序变得很重要（见下文 ❷）。
- 2. ❷ 只有关键变量和两个派生变量会写入新数据集。该数据集将针对每个原始观测，为每个未知变量各保留一个观测。
- 3. ❸ VARVALUE 的长度必须足够大，以存储可能的最长格式化值。
- 4. 临时数组保存感兴趣变量的名称。维度必须足够大。在此示例中，维度为三就足够了。
- 5. 使用 DO UNTIL 循环遍历未知数量的变量，并将其名称存储在数组中。由于此时我们处理的是元数据，因此只需处理一次此信息。
- 6. VNEXT 例程检索连续的变量名，并将名称和类型存储在变量 NAME 和 TYPE 中。
- 7. 所有字符变量（TYPE='C'）都会被选择加载到变量名数组中，但 DATA 步中使用的变量除外。
- 8. VNAMEX 函数用于将变量 NAME 中包含的值存储到名称列表数组中。该函数允许恢复 NAME 的解析值。VNAME 函数原本会存储未解析的值（NAME）。
- 9. 从数组中恢复变量名并存储在 VARNAME 中。VARNAME 现在包含其代码也需要恢复的变量名。VVALUEX 函数不仅检索该变量的值，还检索该变量的格式化值。由于我们需要格式化值，因此这非常完美。

**VIEWTABLE Work.Namelist**

| Obs | lname | fname | 变量 | 值 |
|---|---|---|---|---|
| 1 | Adams | Mary | sex | 女性 |
| 2 | Adams | Mary | race | 黑人 |
| 3 | Adams | Mary | symp | 咳嗽 |
| 4 | Adamson | Joan | sex | 女性 |
| 5 | Adamson | Joan | race | 黑人 |
| 6 | Adamson | Joan | symp | 呼吸急促 |
| 7 | Alexander | Mark | sex | 男性 |
| 8 | Alexander | Mark | race | 白人 |
| 9 | Alexander | Mark | symp |  |
| 10 | Antler | Peter | sex | 男性 |

NAMELIST 数据集将为每个未知变量保留一个观测。VARNAME 包含原始变量名，VARVALUE 包含其格式化值。

通过使用 PROC TRANSPOSE 将这些行转换为列，可以重建原始数据的通用形式。

```sas
proc transpose data=namelist
    out=original(drop=_name_);
    by lname fname;
    id varname;
    var varvalue;
run;
```

- 10. 保存感兴趣变量名称的变量用作 PROC TRANSPOSE 步中的 ID 变量。

转置步骤之后，数据反映了原始数据的形式；不过，编码值已转换为格式化值。

| Obs | lname | fname | sex | race | symp |
|---|---|---|---|---|---|
| 1 | Adams | Mary | 女性 | 黑人 | 咳嗽 |
| 2 | Adamson | Joan | 女性 | 黑人 | 呼吸急促 |
| 3 | Alexander | Mark | 男性 | 白人 |  |
| 4 | Antler | Peter | 男性 | 黑人 | 呼吸急促 |
| 5 | Atwood | Teddy | 男性 |  | 恶心 |

……列表的部分内容未显示……

## 计数函数

COUNT 家族中的函数返回字符串中项的数量。这些字符串可以是字符字符串或单词字符串。每个函数支持三个参数。第一个始终是要搜索的字符串。第二个参数的用法因这些函数而异，而这些函数的真正强大之处和灵活性通过使用第三个参数实现，第三个参数可以取许多不同的值。

- **COUNT** — 统计特定字符串出现的次数
- **COUNTC** — 统计字符字符串中出现或不出现的字符数
- **COUNTW** — 统计字符串中的单词数

COUNTC 和 COUNTW 函数都支持十多个用于第三个参数的修饰符。这些修饰符允许您将字符或数字添加到列表中、从左侧或右侧计数，以及添加多种不同类型的特殊字符。

这些函数也可以在宏语言中使用。这里，COUNTW 函数与 %SYSFUNC 一起使用，以统计列表中的名称数量。

```sas
proc sql noprint;
select lname
    into :namelist separated by '/'
    from advrpt.demog(where=(lname=:'S'));
quit;
%put &namelist;
%put the number of names is %sysfunc(countw(&namelist,/));
```

```
28    %put &namelist;
Saunders/Simpson/Smith/Stubs
29    %put the number of names is %sysfunc(countw(&namelist,/));
the number of names is 4
```

## 另请参见

COUNTW 函数曾在 SAS 论坛帖子 http://communities.sas.com/thread/14720 中使用。

## DIM 函数

DIM 函数旨在返回数组的维度。这意味着它会计数变量；在过去，在如上所示的 COUNTW 函数出现之前，它曾被用于统计列表中的单词数。

```sas
%macro wcount(list);
%* Count the number of words in &LIST;
%global count;
    data _null_;
        array nlist(*) &list;
        call symput('count', dim(nlist));
    run;
%mend wcount;
%wcount(&namelist)
%put The total number of words in &namelist is: &count;
```

这里，我们通过将单词列表用作变量名来欺骗 DIM 函数。然后 DIM 函数会统计这些单词。这种计数方法比上面展示的 COUNTW 函数限制更多，因为单词必须符合 SAS 变量命名约定：列表必须以空格分隔，&COUNT 宏变量被放在全局符号表上，并且需要 DATA 步。
