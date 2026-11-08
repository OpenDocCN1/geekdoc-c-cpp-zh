

要使用这些选项，请将它们放在所应用的数据集名称后面的括号中。虽然数据集选项几乎可以在数据集被引用的任何时候使用，但其中一些选项取决于具体情况，这意味着在应用之前你需要了解该选项的作用。例如，控制数据集读取方式的选项不应用于DATA语句。

在以下示例中，KEEP数据集选项应用于PROC SORT所使用的数据集。

```sas
proc sort data=advrpt.demog(keep= lname fname ssn)
          out=namesonly;
by lname fname;
run;
```

无论ADVRPT.DEMOG中有多少个变量，SORT过程只需要处理KEEP=选项中指定的三个变量。对于SORT过程来说，这可以大大加快处理速度。

数据集选项仅应用于与之关联的数据集。这里，所有变量

```sas
data yr6_7;
  set year2006
      year2007(keep=subject visit labdt);
run;
```

其中，来自YEAR2006的变量都会包含在内。只有来自YEAR2007的变量才会受到KEEP=数据集选项的限制。

当使用数据集列表缩写时，情况并非如此。

```sas
data yr6_7;
  set year:(keep=subject visit labdt);
run;
```

只会从输入数据集（WORK.YEARxxxxxx）中读取这三个变量。变量列表适用于每个输入数据集；因此，如果其中一个或多个输入数据集中不存在某个变量，就会生成错误。

对于许多数据集选项，可以通过使用DATA步语句或系统选项来获得类似的功能。系统选项最为通用（它们适用于所有数据集）；DATA步语句仅适用于该DATA步内的数据集；而数据集选项最为具体，因为它们只适用于特定的数据集。

### 更多信息

有关将数据集选项与PROC SORT一起使用的更多信息，请参见第4.2节。INDSNAME=选项以及IN=数据集选项将在第3.8.2节中讨论。

### 2.1.1 REPLACE和REPEMPTY

由于可以创建一个空（零观测）数据集，我们可能需要控制新表是否替换同名已存在的表。在本例中，假设数据集ADVRPT.CLASS已经存在。由于SASHELP.CLASS数据集中没有年龄>25的观测，因此此DATA步中的WHERE子句始终为false，不会写入任何观测，数据集

```sas
data advrpt.class;
   set sashelp.class;
   where age > 25;
run;
```

ADVRPT.CLASS将被一个空数据集替换。

REPLACE和REPEMPTY数据集选项允许我们控制数据集被替换的条件。

- **REPLACE**：REPLACE=NO阻止替换*永久*数据集。此数据集选项会覆盖同名的系统选项。REPLACE=YES是默认值。
- **REPEMPTY**：确定空数据集是否可以覆盖现有数据集。

为了全面保护，这两个选项通常一起使用。通常我们希望能够替换永久数据集，除非新版本为空。在以下DATA步中，没有AGE大于25的观测，因此将返回零个观测。

```sas
data advrpt.class (replace=yes repempty=no);
   set sashelp.class;
   where age > 25;
run;
```

但是，由于REPEMPTY=NO，数据集ADVRPT.CLASS将不会被替换。

传统上，当DATA语句漏写分号时，用空数据集覆盖已有观测的数据集这一问题尤其棘手。在以下DATA步中，由于缺少分号❶，SET语句被掩盖，从而创建了*三个*空数据集（ADVRPT.VERYIMPORTANT、WORK.SET和SASHELP.CLASS）。

```sas
options DATASTMTCHK=NONE;
data advrpt.VeryImportant ❶
   set sashelp.class;
run;
```

❶ 缺少分号会使SAS将SET语句视为DATA语句的一部分。结果是没有任何输入数据集；因此，创建的数据集将没有变量或观测。

❷ DATASTMTCHK系统选项通过不允许使用诸如SET和MERGE之类的名称创建数据集来保护我们免于此问题。将DATASTMTCHK设置为NONE会移除这种保护。

```sas
options DATASTMTCHK=NONE; ❷
data advrpt.VeryImportant (replace=yes repempty=no) ❸
   set sashelp.class;
run;
```

❸ REPEMPTY=NO选项将保护我们非常重要的数据集，但遗憾的是不能保护SASHELP.CLASS数据集。

除非有令人信服的理由，否则我认为DATASTMTCHK的值不应设置为NONE。如果必须更改该选项，请使用REPLACE和REPEMPTY数据集选项❸来提供一些保护。

### 2.1.2 密码保护

数据集可以同时进行加密和密码保护。密码和加密数据集选项包括：

- **ALTER**：更改数据集的密码
- **ENCRYPT**：加密数据集
- **PW**：指定密码
- **PWREQ**：密码请求窗口
- **READ**：读取数据集的密码
- **WRITE**：写入数据集的密码

以下DATA步创建的数据集不仅经过加密，而且读取和写入需要不同的密码。

```sas
data advrpt.pword(encrypt=yes pwreq=yes
                  read=readpwd write=writepwd);
   DB='DEApp'; UID='MaryJ'; pwd='12z3'; output;
   DB='p127';  UID='Mary';  pwd='z123'; output;
run;
proc print data=advrpt.pword;
   run;
```

在PROC PRINT显示受保护的数据集之前，将出现以下对话框，要求输入READ密码。

![](img/4b16455363806a3241267bf9f49ba5d1_69_0.png)

虽然这些密码保护在SAS内部可能很有用，但受保护的文件仍然容易被SAS外部的工具删除或篡改。包含ENCRYPT选项可以增加一层针对非SAS工具的保护。

### 更多信息

更多关于密码保护的信息，包括使用包含密码的数据集（如本节中使用的数据集），将在第5.4.2节中说明。

### 2.1.3 KEEP、DROP和RENAME选项

在DATA步中使用KEEP、DROP或RENAME时，你可以选择使用数据集选项或DATA步语句。当创建或读取多个数据集时，DATA步语句适用于所有创建的数据集，而数据集选项可以应用于特定的数据集。一般来说，当你有选择余地时，数据集选项优于语句，因为数据集选项可以让你更好地控制，并且代码通常更清晰。

KEEP语句在功能上与DROP语句相反。以下关于KEEP语句和KEEP=数据集选项的讨论同样适用于DROP语句和DROP=数据集选项。我在这里演示KEEP语句和KEEP=数据集选项，是因为我承认自己对DROP语句和DROP=数据集选项有偏见。DROP语句和DROP=数据集选项工作得很好，它们都能完全实现预期功能，并且在需要保留的变量列表很长而需要删除的变量列表很短时，两者都可以为程序员节省打字量。然而，KEEP通过记录程序员确实需要继续考虑哪些变量，向程序员传达了更多信息。

以下示例突出显示了KEEP语句和KEEP=数据集选项之间的区别。下面的KEEP语句❶仅应用于新数据集（WORK.LABS），并且绝不会影响程序数据向量（PDV），也不会影响从输入数据集（ADVRPT.LAB_CHEMISTRY）读取哪些变量。

```sas
data labs;
   set advrpt.lab_chemistry;
   keep subject visit labdt; ❶
   if sodium>'142'; ❷
run;
```

- ❶ KEEP语句的变量列表应用于新的输出数据集。
- ❷ IF语句在整个观测被读取并加载到PDV之后执行。

使用KEEP语句❶与在DATA语句中的数据集上指定KEEP=选项❸完全相同。然而，SET语句上的KEEP=选项❹会在PDV构建之前应用。只有列出的那些变量才会从输入数据集读取并包含在PDV中。

```sas
data labs(keep=subject visit labdt); ❸
   set advrpt.lab_chemistry(keep=subject visit labdt sodium ❹
                            where=(sodium>'142')); ❺
run;
```

- ❸ KEEP=数据集选项仅影响哪些变量将被写入新数据集。
- ❹ 在SET语句中，KEEP=数据集选项应用于输入数据集；因此，该变量列表影响哪些变量会出现在PDV上。由于本示例中SODIUM在WHERE=子句❺中使用，即使它不会被写入新数据集，KEEP=数据集选项也必须包含SODIUM。
- ❺ WHERE=过滤器作为数据集选项指定，并在观测被读取之前应用。

RENAME选项允许您在读取或写入变量时更改变量名。与RENAME语句一样，其语法形式为oldname=newname。将RENAME=选项放在SET语句❻上会在变量写入PDV之前更改其名称。

