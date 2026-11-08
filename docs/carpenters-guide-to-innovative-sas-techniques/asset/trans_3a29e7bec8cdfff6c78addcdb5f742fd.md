
## 选项、数据集

| 选项 | 主要描述见： | 也出现于： |
| --- | --- | --- |
| ALTER | 2.1.2 | 5.4.2 |
| DROP | 2.1.3 | 5.1 |
| ENCRYPT | 2.1.2 | 5.4.2 |
| FIRSTOBS | 2.1.4 | 3.1.4, 3.1.5 |
| KEEP | 2.1.3 | 2.1, 2.3.2, 3.1.4, 3.1.5, 4.2, 5.2,<br>11.1.2, 12.7, 13.5.2 |
| IDXNAME | 5.3.4 | |
| IDXWHERE | 5.3.4 | |
| IN | | 3.8.2, 3.7.1 |
| INDEX | 5.3.2 | |
| OBS | 2.1.4 | 8.5.2 |
| PW | 2.1.2 | |
| PWREQ | 2.1.2 | 5.4.2 |
| READ | 2.1.2 | 5.4.2 |
| RENAME | 2.1.3 | 3.1.4, 3.1.5, 3.7.2, 5.1, 6.4, 12.7 |
| REPEMPTY | 2.1.1 | |
| REPLACE | 2.1.1 | |
| SORTEDBY | 4.4 | |
| WHERE | | 2.1.3, 2.1.4d, 2.2.2, 3.7.2, 5.1,<br>7.7, 7.8, 11.5.3, 13.2.3, 13.6,<br>14.1.1 |
| WRITE | 2.1.2 | 5.4.2 |

## 过程：步骤、语句和选项

### 过程

| 语句和选项 | 主要描述见： | 也出现于： |
| --- | --- | --- |
| *通常（跨过程）* | | |
| &nbsp;&nbsp;CLASS | 7.1 | 7.1.2, 8.2.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;DESCENDING | 7.1.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;GROUPINTERNAL | 7.1.2 | |
| &nbsp;&nbsp;&nbsp;&nbsp;MISSING | 7.1.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;ORDER | 7.1.3 | |
| &nbsp;&nbsp;EXCLUSIVE | 12.1 | |
| &nbsp;&nbsp;MISSING | 2.10.5, 7.1.1 | |
| &nbsp;&nbsp;ORDER | 2.6.2, 8.1.5 | 2.5.5, 8.4.5 |
| &nbsp;&nbsp;PRELOADFMT | 12.1 | 2.5.5 |
| BOXPLOT | 10.1.1 | |
| CATALOG | | |
| &nbsp;&nbsp;CONTENTS | | 12.9.3 |
| &nbsp;&nbsp;COPY | | 13.9.2 |
| &nbsp;&nbsp;ENTRYTYPE | | 13.9.2 |
| &nbsp;&nbsp;DELETE | 13.9.2 | |
| &nbsp;&nbsp;FORCE | 13.9.2 | |
| &nbsp;&nbsp;SELECT | | 13.9.2 |
| COMPARE | 5.1 | |
| &nbsp;&nbsp;COMPARE | 5.1 | |
| &nbsp;&nbsp;OUT | 5.1 | |
| &nbsp;&nbsp;OUTBASE | 5.1 | |
| &nbsp;&nbsp;OUTCOMP | 5.1 | |
| &nbsp;&nbsp;OUTNOEQUAL | 5.1 | |
| CONTENTS | | 2.6.1, 5.3.1, 13.8.3 |
| &nbsp;&nbsp;_ALL_ | 13.8.3 | |
| &nbsp;&nbsp;OUT | 13.8.3 | |
| &nbsp;&nbsp;NOPRINT | | 13.8.3 |
| &nbsp;&nbsp;VARNUM | 2.6.1 | |
| DATASETS | | 2.6.1 |
| &nbsp;&nbsp;AGE | 5.6.2 | |
| &nbsp;&nbsp;CHANGE | 5.6.2 | |
| &nbsp;&nbsp;CONTENTS | | 2.6.1 |
| &nbsp;&nbsp;DELETE | 5.5 | |
| &nbsp;&nbsp;INDEX CREATE | 5.3.2 | 5.3.3, 6.6 |
| &nbsp;&nbsp;INDEX DELETE | 5.3.2 | 5.3.3 |
| &nbsp;&nbsp;KILL | 5.5 | 14.4.5 |
| &nbsp;&nbsp;MODIFY | 5.3.2 | 2.6.1, 5.3.3, 6.6 |
| &nbsp;&nbsp;NOLIST | 5.5 | 5.6.2, 6.6 |
| DELETE | 5.5 | |
| EXPORT | 1.2 | 1.4.2, 11.2.2 |
| &nbsp;&nbsp;SHEET | 1.2.3 | 1.2.1, 11.2.2 |
| FCMP | 15.2 | 12.5.5 |
| &nbsp;&nbsp;DELETEFUNC | 15.2.5 | |
| &nbsp;&nbsp;ENDSUB | 15.2.1 | 12.5.5 |
| &nbsp;&nbsp;FUNCTION | 15.2.1 | 12.5.5 |
| &nbsp;&nbsp;OUTLIB | 15.2.2 | |
| &nbsp;&nbsp;RETURN | 15.2.1 | 12.5.5 |
| &nbsp;&nbsp;RUN_MACRO | 15.2.3 | |
| &nbsp;&nbsp;SUBROUTINE | 15.2.3 | |
| FORMAT | | |
| &nbsp;&nbsp;CNTLIN | 12.7 | 6.5, 6.7.3, 12.3.2 |
| &nbsp;&nbsp;CNTLOUT | 12.7 | |
| &nbsp;&nbsp;DEFAULT | | 12.5.4, 12.5.5 |
| &nbsp;&nbsp;格式作为标签 | 12.5.1 | 12.5.2, 12.5.3, 12.8 |
| &nbsp;&nbsp;函数作为标签 | 12.5.5 | |
| &nbsp;&nbsp;INVALUE | | 12.5.3 |
| &nbsp;&nbsp;LIBRARY | 12.9.3 | |
| &nbsp;&nbsp;NOTSORTED | 12.4 | |
| &nbsp;&nbsp;MULTILABEL | 12.3 | |
| &nbsp;&nbsp;PICTURE | 12.2 | |
| &nbsp;&nbsp;&nbsp;&nbsp;DATATYPE | 12.2.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;指令 | 12.2.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;MULT | 12.2.3 | |
| &nbsp;&nbsp;&nbsp;&nbsp;PREFIX | 12.2.3 | |
| &nbsp;&nbsp;&nbsp;&nbsp;ROUND | 12.2.2 | |
| &nbsp;&nbsp;REGEXP | 12.5.4 | |
| &nbsp;&nbsp;_SAME_ | 12.5.4 | |
| &nbsp;&nbsp;VALUE | 12.7 | 2.6.2, 3.6.6, 7.1.2, 8.1.1, 8.1.5, 11.3.4, 11.3.5, 11.4.4, 11.5.1, 11.5.2, 12.1, 12.8 |
| FREQ | | |
| &nbsp;&nbsp;NLEVELS | 8.3 | 2.5.6, 2.9.4, 10.3 |
| &nbsp;&nbsp;OUTPUT | 8.3.2 | |
| &nbsp;&nbsp;ALL | 8.3.1 | |
| &nbsp;&nbsp;SPARSE | 8.3.1 | 2.5.6 |
| &nbsp;&nbsp;TABLE | | |
| &nbsp;&nbsp;&nbsp;&nbsp;ALL | | 8.3.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;CHISQ | | 8.3.1 |
| &nbsp;&nbsp;&nbsp;&nbsp;PLOTS | 10.3 | |
| GFONT | 10.2.1 | |
| GKPI | 10.2.4 | |
| GPLOT | 10.1.2 | |
| IMPORT | 1.2 | 14.1.2 |
| &nbsp;&nbsp;DATAROW | 1.2.3 | |
| &nbsp;&nbsp;DBMS | | 14.1.2 |
| &nbsp;&nbsp;GETNAMES | 1.2.3 | 1.2.5, 14.1.2 |
| &nbsp;&nbsp;GUESSINGROWS | 1.2.3 | |
| &nbsp;&nbsp;MIXED | 1.2.3 | 14.1.2 |
| &nbsp;&nbsp;RANGE | 1.2.3 | 1.2.5 |
| &nbsp;&nbsp;SCANTEXT | 1.2.3 | 14.1.2 |
| &nbsp;&nbsp;SCANTIME | 1.2.3 | 14.1.2 |
| &nbsp;&nbsp;SHEET | 1.2.3 | 1.2.1, 14.1.2 |
| &nbsp;&nbsp;TEXTSIZE | 1.2.3 | 14.1.2 |
| &nbsp;&nbsp;USEDATE | | |
| MEANS/SUMMARY | 第 7 章 | 2.5.3, 2.5.4, 2.5.5, 13.3.1 |
| &nbsp;&nbsp;CHARTTYPE | 7.6 | |
| &nbsp;&nbsp;CLASS | | |
| &nbsp;&nbsp;&nbsp;&nbsp;EXCLUSIVE | 12.1.3 | |
| &nbsp;&nbsp;&nbsp;&nbsp;MLF | | 12.3.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;PRELOADFMT | 12.1.3 | |
| &nbsp;&nbsp;CLASSDATA | 7.9 | 2.5.4 |
| &nbsp;&nbsp;COMPLETETYPES | 7.10 | 2.5.3, 12.1.3 |
| &nbsp;&nbsp;EXCLUSIVE | 7.9 | |
| &nbsp;&nbsp;MISSING | 7.1.1 | |
| &nbsp;&nbsp;NWAY | | 7.6, 7.7 |
| &nbsp;&nbsp;OUTPUT | 7.3 | 7.1 |
| &nbsp;&nbsp;&nbsp;&nbsp;AUTONAME | 7.2 | 5.3.3, 7.4.3 |
| &nbsp;&nbsp;&nbsp;&nbsp;AUTOLABEL | 7.2 | |
| &nbsp;&nbsp;&nbsp;&nbsp;GROUPID | 7.4.2 | |
| &nbsp;&nbsp;&nbsp;&nbsp;LEVELS | 7.2, 7.11 | |
| &nbsp;&nbsp;&nbsp;&nbsp;MAXID | 7.4.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;MINID | 7.4.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;WAYS | 7.2, 7.11 | |
| &nbsp;&nbsp;TYPES | 7.8 | |
| &nbsp;&nbsp;WAYS | 7.7 | |
| OPTIONS | | 14.3.1 |
| OPTLOAD | 14.1.3 | |
| OPTSAVE | 14.1.3 | |
| PRINT | 8.5 | 11.5.4, 11.7.1 |
| &nbsp;&nbsp;BY | 8.5.1 | 11.5.4 |
| &nbsp;&nbsp;ID | 8.5.1 | 11.5.4 |
| &nbsp;&nbsp;STYLE | 8.5.2 | 11.5.4 |
| PWENCODE | 5.4.1 | |
| REG | | 9.3.1, 9.3.2, 9.4 |
| REPORT | 8.4 | 2.5.5, 10.2.4, 11.2.3, 11.3.1, 11.3.2, 11.3.3, 11.3.4, 11.3.5, 11.4.1, 11.5.3 |
| &nbsp;&nbsp;绝对列引用 | 8.4.2 | 8.4.3, 8.4.5 |
| &nbsp;&nbsp;别名规范 | 8.4.3 | 8.4.2, 8.4.5, 8.4.7, 12.1.1 |
| &nbsp;&nbsp;CALL DEFINE | 8.4.7 | 10.2.4, 11.4.1, 11.5.3 |
| &nbsp;&nbsp;COMPLETECOLS | 12.1 | |
| &nbsp;&nbsp;COMPLETEROWS | 12.1, 12.1.1 | 2.5.5 |
| &nbsp;&nbsp;&nbsp;&nbsp;计算块 | 8.4.3 | |
| &nbsp;&nbsp;&nbsp;&nbsp;CONTENTS | 11.4.3 | |
| &nbsp;&nbsp;&nbsp;&nbsp;DEFINE | | |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EXCLUSIVE | 12.1.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NOPRINT | 8.4.4 | 8.4.6 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PRELOADFMT | 12.1.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ORDER | 8.4.5 | 8.4.8 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NOZERO | 8.4.8 | |
| &nbsp;&nbsp;&nbsp;&nbsp;LINE | 8.4.10 | 8.4.6, 11.3.2, 11.3.3, 11.3.4 |
| &nbsp;&nbsp;&nbsp;&nbsp;STYLE 覆盖 | 8.4.6 | 8.4.8, 11.5.3 |
| SHEWHART | 10.1.3 | |
| SORT | 4.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;DUPOUT | 4.1.2 | |
| &nbsp;&nbsp;&nbsp;&nbsp;EQUALS | 4.1.6 | |
| &nbsp;&nbsp;&nbsp;&nbsp;FORCE | 4.1.5 | |
| &nbsp;&nbsp;&nbsp;&nbsp;NODUPKEY | | 2.5.1, 6.7.1 |
| &nbsp;&nbsp;&nbsp;&nbsp;NODUPLICATES (NODUPREC) | 4.1.1 | 2.9.1, 4.1.2, 4.4 |
| &nbsp;&nbsp;&nbsp;&nbsp;SORTSEQ | 4.1.4 | |
| &nbsp;&nbsp;&nbsp;&nbsp;TAGSORT | 4.1.3 | |
| SQL | 1.5 | 2.8.1, 2.9.3, 3.7.4, 5.2, 5.4.2, 11.2.2, 11.2.3, 11.4.1, 11.4.3, 13.5.1, 13.5.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;CONNECT | 1.5.1 | 5.4.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;CREATE INDEX | 5.3.2 | 5.3.3 |
| &nbsp;&nbsp;&nbsp;&nbsp;DESCRIBE | 13.8.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;DISCONNECT | 1.5.1 | 5.4.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;DISTINCT | 2.9.3 | |
| &nbsp;&nbsp;&nbsp;&nbsp;DROP TABLE | 5.5 | |
| &nbsp;&nbsp;&nbsp;&nbsp;ORDER BY | | 2.9.3 |
| &nbsp;&nbsp;&nbsp;&nbsp;UNION | 2.8.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;WHERE | 2.2.2 | |
| TABULATE | 8.1 | 11.4.4, 11.5.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;CLASS | 8.1.1 | 11.5.2 |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EXCLUSIVE | 12.1.2 | |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MLF | 12.3.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PRELOADFMT | 12.1.2 | |
| &nbsp;&nbsp;&nbsp;&nbsp;CLASSDATA | 8.1.4 | |
| &nbsp;&nbsp;&nbsp;&nbsp;CLASSLEV | 8.1.3 | 11.4.4 |
| &nbsp;&nbsp;&nbsp;&nbsp;EXCLUSIVE | 8.1.4 | |
| &nbsp;&nbsp;&nbsp;&nbsp;KEYLABEL | 8.1.1 | |
| &nbsp;&nbsp;&nbsp;&nbsp;KEYWORD | 8.1.3 | |
| &nbsp;&nbsp;&nbsp;&nbsp;ORDER | 8.1.5 | |
| &nbsp;&nbsp;&nbsp;&nbsp;TABLE | 8.1.1 | 11.5.2 |

