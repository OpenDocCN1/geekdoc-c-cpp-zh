
或者，可以使用 `IN` 方法稍后实例化并加载矩阵：

```sas
dcl double a[2];
dcl package m(2,2);
method init();
/* 加载值 */
a:=(1, 9, 4, 16);
end;
```

使用矩阵的 `IN` 方法从表中加载数据：

```sas
data x;
v1=1;v2=2;output;
v1=4;v2=16;output;
run;
```

将行列获取变量：

```sas
proc sql noprint;
select nobs
into :rows :columns
from dictionary.tables
where libname='WORK'
and memename='X';
quit;
```

```sas
proc ds2;
data _null;
  varray double a[2];
  dcl package m(&rows,&columns)
  method run();
  /* 读取数据，从 varray 加载矩阵的每一行*/
  set x;
  m.append(a, _n);
enddata;
run;
```

### 5.5.1.3 操作矩阵值

使用矩阵包可用的方法之一对矩阵进行操作。数据可以从矩阵移动到声明数组或变量数组。如果使用了变量数组，数据将加载到 `PDV` 变量并成为程序结果集的一部分。

在以下示例中，值被加载到数组 `a`，数组 `a` 的元素值打印在 `SAS` 日志中。随后，使用 `IN` 方法从数组值填充矩阵。然后使用 `TRANS` 方法转置矩阵 `m`，并通过 `TOARRAY` 方法将其元素传回数组 `a`。数组 `a` 的元素再次写入 `SAS` 日志。最后，对矩阵 `m` 的所有元素执行平方根变换，并将值再次通过 `TOARRAY` 方法传给数组 `a`。

```sas
proc ds2;
data _null;
  dcl double a[2, 2];
  dcl package m(2,2);
method init();
  a:=1, 9, 4, 16);
  put 'before: ' a[*]=;
  m.append(a);
  m.trans(a);
  m.toarray(a);
  put 'Trans: ' a[*]=;
  m.sqrt(sqrt);
  m.toarray(a);
  put 'SQRT ' a[*]=;
enddata;
run;
quit;
```

# 掌握 SAS DS2 过程：高级数据处理技术

`SAS` 日志：

| 处理前 | a[1,1]=1 a[1,2]=9 a[2,1]=4 a[2,2]=16 |
| 转置: | a[1,1]=1 a[1,2]=4 a[2,1]=9 a[2,2]=16 |
| 根号: | a[1,1]=1 a[1,2]=2 a[2,1]=3 a[2,2]=4 |

以下示例展示了类似的处理，从数据表中加载数据，使用方法将数据从矩阵移动到 `VARARRAY`，并将结果写入 `DS2` 程序的结果集：

```sas
proc ds2;
data;
  dcl varchar(7) Timing;
  dcl package matrix m(2,2);
  vararray double a[2] vl2;
  vararray double v[2, 2] w x y z;
  dcl double b[2,2];
  drop v1 v2;
  method run();
  /* 读取数据，从 vararray 加载矩阵的每一行*/
    set x;
    m.in(a, n);
    m.tovarray(b);
  end;
  method term();
  Timing='Before:';
    m.tovarray(v);
    output;
  Timing='Trans:';
    m=m.trans();
    m.tovarray(v);
    output;
  Timing='SQRT:';
    m=m.sqrt();
    m.tovarray(v);
    output;
  end;
ata;
run;
quit;
```

图 5.13：使用矩阵包处理后的数据

| 计时 | w | x | y | z |
| 处理前: | 1 | 9 | 4 | 16 |
| 转置: | 1 | 4 | 9 | 16 |
| 根号: | 1 | 2 | 3 | 4 |

## 5.5.2 矩阵包示例

我们的车队正准备为今年车队的维护订购所需的液体。数据集 `crs_fleet` 包含了车队中车辆的信息：

图 5.14：`crs_fleet` 数据集包含的数据

| 观测值 | 品牌 | 型号 | ボディ类型 | 年份 | 库存 | 机油 | 冷却 | 变速箱 | 差速器 |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Ford | F550 | 皮卡车 | 2015 | 24 | 7.0 | 26.7 | | 17.5 | 5.9 |
| 2 | Ford | Expedition | 全尺寸 SUV | 2015 | 12 | 6.0 | 18.5 | | 13.1 | 3.6 |
| 3 | Dodge | Ram Proaster 3500 | 货运箱 | 2015 | 20 | 6.0 | 10.6 | | 9.0 | 4.8 |
| 4 | GMC | Yukon XL | 全尺寸 SUV | 2015 | 12 | 8.0 | 17.4 | | 11.4 | 5.5 |
| 5 | Smart | For Two | 微型 | 2015 | 144 | 3.6 | 4.5 | | 2.5 | 0.0 |
| 6 | Land Rover | Range Rover | 全尺寸 SUV | 2010 | 48 | 6.5 | 16.0 | | 10.5 | 1.5 |

首先，我们创建一个六行四列的矩阵，代表所有车辆的液体容量，并创建一个一行六列的第二个矩阵，代表每种车辆的库存。下一步是这两个矩阵的乘法。结果是一个一行四列的矩阵，包含了今年维护所需的每种液体的总量。

### 5.5.2.1 将数据读入/导出矩阵

由于使用数组 `arrays` 在矩阵包之间传输数据更为方便，因此对于我们创建的每个矩阵，我们都会创建一个相应的数组或变量。我们将使用 `RUN` 方法来加载容量矩阵和车辆库存。然后，在 `TERM` 方法中，我们将车辆库存加载到单元矩阵中，执行乘法，并将所有值结果转移到体积数组中，向上取入到最近的整数，并输出结果集。

```sas
proc ds2;
title1 '今年维护所需的液体：';
title2 '所有体积均为加仑：';
data;
* 矩阵 *
* 六种车辆类型，每种 4 种容量 */
dcl package matrix m_caps(6,4);
* 每种类型维护的数量 */
dcl package matrix m_units(1,6);
* 需要购买的每种液体总量 */
dcl package matrix m_fluid_reg(1,4);
* 数组 /
* 每辆车 4 种容量 */
vararray double a[4] Oil Cooling Transmission Differential;
* 每种类型维护的数量 */
dcl double a_units[1] Inventory;
* 需要购买的每种液体总量 */
vararray double a_vals[4] Oil Cooling Transmission Differential;
keep Oil Cooling Transmission Differential;
```

```sas
method run();
  set curs.out_fleet;
/* 从 vararray逐行加载容量矩阵 */
  m_caps.in(a_caps, n);
/* 用库存值加载单元数组 */
  a_units[n]=Inventory;
end;
method term();
  dcl int i;
/* 从单元数组加载单元矩阵 */
  m_units.in(a_units);
  /* 所有矩阵加载完成后，进行计算 */
  m_vols_reg=units.mlt(m_caps);
/* 将结果加载到体积数组 */
  m_vols_req.toarray(a_vols);
/* 今年每辆车要换 4 次机油 */
/* 冷却液和变速箱油是夸司，转换为加仑 */
```
