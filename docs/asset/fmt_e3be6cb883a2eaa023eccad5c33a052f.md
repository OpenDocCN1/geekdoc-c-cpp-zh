
```
data EmpsAUC;
merge EmpsAU PhoneC;
by EmpID;
run;
```

`EmpID` 是否与 PDV 中的 `EmpID` 相同？

否

PDV

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| Kylie | F | 121151 | |

# 执行

| 姓名 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2)5555-1667 |
| Birin | M | 121152 | 121153 | +61(2)5555-1348 |

```
data EmpsAUC;
merge EmpsAU PhoneC;
by EmpID;
run;
重新初始化 PDV
```

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| | | | |

# 执行

| 姓名 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2)5555-1667 |
| Birin | M | 121152 | 121153 | +61(2)5555-1348 |

```
data EmpsAUC;
merge EmpsAU PhoneC;
by EmpID;
run;
```

从每个匹配的数据集读取一个观测值

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| Birin | M | 121152 | +61(2)5555-1667 |

# 执行

| EmpsAU | PhoneC |
| --- | --- |
| 姓名 | 性别 | EmpID | 电话 |
| Togar | M | 121150 | 121150 +61(2) 5555-1795 |
| Kylie | F | 121151 | 121152 +61(2) 5555-1667 |
| Birin | M | 121152 | 121153 +61(2) 5555-1348 |

```
data EmpsAUC;
  merge EmpsAU PhoneC;
  by EmpID;
run;
```

隐式输出：

隐式返回；

| PDV |
| --- |
| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| Birin | M | 121152 | +61(2)5555-1667 |

# 执行

| EmpsAU | PhoneC |
| --- | --- |
| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| Togar | M | 121150 | 121150 +61(2) 5555-1795 |
| Kylie | F | 121151 | 121152 +61(2) 5555-1667 |
| Birin | M | 121152 | 121153 +61(2) 5555-1348 |

```
data EmpsAUC;
  merge EmpsAU PhoneC;
  by EmpID;
run;
```

`EmpID` 是否与 PDV 中的 `EmpID` 相同？

否

PDV |

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| Birin | M | 121152 | +61(2)5555-1667 |

# 执行

| 姓名 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2)5555-1667 |
| Birin | M | 121152 | 121153 | +61(2)5555-1348 |

```
data EmpsAUC;
  merge EmpsAU PhoneC;
  by EmpID;
run;
```

| | |别 | EmpID | 电话 |
| --- | --- | --- | --- |

# 执行

| 姓名 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2)5555-1667 |
| Birin | M | 121152 | 121153 | +61(2)5555-1348 |

```
data EmpsAUC;
merge EmpsAU PhoneC;
by EmpID;
run;
重新初始化 PDV;
```

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |

# 执行

| 姓名 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2)5555-1667 |
| Birin | M | 121152 | 121153 | +61(2)5555-1348 |

```
data EmpsAUC;
merge EmpsAU PhoneC;
by EmpID;
run;
```

从适当的数据集读取观测值

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| | | 121153 | +61(2)5555-1348 |

# 执行

| EmpsAU | PhoneC |
| --- | --- |
| 姓名 | 性别 | EmpID | EmpID | 电话 |
| Togar | M | 121150 | 121150 +61(2) 5555-1795 |
| Kylie | F | 121151 | 121152 +61(2) 5555-1667 |
| Birin | M | 121152 | 121153 +61(2) 5555-1348 |

```
data EmpsAUC;
  merge EmpsAU PhoneC;
  by EmpID;
  隐式输出：
  隐式返回；
```

| PDV | |
| --- | --- |
| 姓名 | 性别 | EmpID | 电话 |
| | | 121153 +61(2)5555-1348 |

# 执行

| EmpsAU | PhoneC |
| --- | --- |
| 姓名 | 性别 | EmpID | EmpID | 电话 |
| Togar | M | 121150 | 121150 +61(2) 5555-1795 |
| Kylie | F | 121151 | 121152 +61(2) 5555-1667 |
| Birin | M | 121152 | 121153 +61(2) 5555-1348 |

```
data EmpsAUC;
  merge EmpsAU PhoneC;
  by EmpID;
run;
```

`EmpID` 是否与 PDV 中的 `EmpID` 相同？

否

PDV |

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| Birin | M | 121152 | +61(2)5555-1667 |

# 执行

| 姓名 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2)5555-1667 |
| Birin | M | 121152 | 121153 | +61(2)5555-1348 |

# Emps 结果

| 姓名 | 性别 | EmpID | 电话 |
| --- | --- | --- | --- |
| Togar | M | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | |
| Birin | M | 121152 | +61(2)5555-1667 |
| | | 121153 | +61(2)5555-1348 |

最终结果包含匹配项和不匹配项。

* 匹配项是包含两个输入数据集数据的观测值。
* 不匹配项是仅包含一个数据集数据的观测值。

# 10.11 测验

在最终集合 `EmpsAUC` 中有多少观测值被认为是不匹配项？

+ a. 1
b. 2
c. 3
d. 4

# 执行

| 名字 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2)5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2)5555-1667 |
| Birin | M | 121152 | 121153 | +61(2)5555-1348 |

```
data EmpsAU(in=Emps)
  PhoneC(in=Cell);
  by EmpID;
run;
```

| 名字 | 性别 | EmpID | Emps | 电话 | Cell |
| --- | --- | --- | --- | --- | --- |
| Togar | M | 121150 | 1 | +61(2)5555-1795 | 1 |

# 执行

| 名字 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2) 5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2) 5555-1667 |
| Birin | M | 121152 | 121153 | +61(2) 5555-1348 |

```
data EmpsAUC;
merge EmpsAU(in=Emps)
PhoneC(in=Cell);
by EmpID;
run;
```

| 名字 | 性别 | EmpID | Emps | 电话 | Cell |
| --- | --- | --- | --- | --- | --- |
| Kylie | F | 121151 | 1 | | 0 |

# 10.12 测

`Emps` 和 `Cell` 的值分别？

| 名字 | 性别 | EmpID | EmpID | 电话 |
| --- | --- | --- | --- | --- |
| Togar | M | 121150 | 121150 | +61(2) 5555-1795 |
| Kylie | F | 121151 | 121152 | +61(2) 5555-1667 |
| Birin | M | 121152 | 121153 | +61(2) 5555-1348 |

```
data EmpsAUC;
merge EmpsAU(in=Emps)
PhoneC(in=Cell);
by EmpID;
run;
```

| 名字 | 性别 | EmpID | Emps | 电话 | Cell |
| --- | --- | --- | --- | --- | --- |
| Birin | M | 121152 | 1 | +61(2) 5555-1667 | 1 |

# 10.6 合并数据集非匹配项

## PDV 结果

| 名字 | 性别 | EmpID | Emps | 电话 | Cell |
| --- | --- | --- | --- | --- | --- |
| Togar | M | 121150 | 1 | +61(2) 5555-1795 | 1 |
| Kylie | F | 121151 | 1 | | 0 |
| Birin | M | 121152 | 1 | +61(2) 5555-1667 | 1 |
| | | 121153 | 0 | +61(2) 5555-1348 |

使用 `IN=` 数据集选项创建的变量在执行期间可用，但不会写入 SAS 数据集。

# 10.13 测

在 `DATA` 语句中添加哪个 `IF` 语句可以输出匹配项？

- a. `if Emps=1 and Cell=0;`
- b. `if Emps=1 and Cell=1;`
- c. `if Emps=1;`
- d. `if Cell=0;`

# 仅匹配项

```
data EmpsAUC;
  merge EmpsAU(in=Emps)
  PhoneC(in=Cell);
  by EmpID;
  if Emps=1 and Cell=1;
run;
```

`IF` 语句控制哪些观测值被 `DATA` 语句进一步处理。在这个例子中，唯一的处理是 `DATA` 语句底部的隐含输出。因此，如果条件为真，观测值被写入数据集。如果条件为假，观测值不写入 SAS 数据集。

该 `IF` 语句可以重写为：

```
if Emps and Cell;
```

# 仅 Emps 的非匹配项

```
data EmpsAUC;
  merge EmpsAU(in=Emps)
  PhoneC(in=Cell);
  by EmpID;
  if Emps=1 and Cell=0;
run;
```

该 `IF` 语句可以重写为：

```
if Emps and not Cell;
```

# 仅 PhoneC 的非匹配项

```
data EmpsAUC;
  merge EmpsAU(in=Emps)
  PhoneC(in=Cell);
  by EmpID;
  if Emps=0 and Cell=1;
run;
```

该 `IF` 语句可以重写为：

```
if not Emps and Cell;
```

# 所有非匹配项

```
data EmpsAUC;
  merge EmpsAU(in=Emps)
  PhoneC(in=Cell);
  by EmpID;
  if Emps=0 or Cell=0;
run;
```

# EmpsAUC

该 `IF` 语句可以重写为：

```
if not Emps or not Cell;
```

# 10.14 测

编写适当的 `IF` 语句以创建所需的数据。

| X | Y | W | X | Y | Z | W |
| --- | --- | --- | --- | --- | --- | --- |
| | 30 | 40 | | 2 | | 60 |

期望的 SAS 数据集

> `if A=1 and B=0;`
>
> 或者
>
> `if A and not B;`

# 输出到多个数据集

`OUTPUT` 语句可以在 `DATA` 语句中将观测值写入特定的数据集。

```
data EmpsAUC EmpsOnly PhoneOnly;
merge EmpsAU(in=Emps)
PhoneC(in=Cell);
if Emps=1 and Cell=1
then output EmpsAUC;
else if Emps=1 and Cell=0
then output EmpsOnly;
else if Emps=0 and Cell=1
then output PhoneOnly;
run;
```

# 多对多合并（自学）

`PROC SQL` 结果：

| First | Gender | Phone | 电话 |
| --- | --- | --- | --- |
| Togar | M | AU | +61 (2) 5555-1500 |
| Togar | M | AU | +61 (2) 5555-1600 |
| Togar | M | AU | +61 (2) 5555-1700 |
| Kylie | F | AU | +61 (2) 5555-1500 |
| Kylie | F | AU | +61 (2) 5555-1600 |
| Kylie | F | AU | +61 (2) 5555-1700 |
| Stacey | F | US | +1 (305) 555-1500 |
| Stacey | F | US | +1 (305) 555-1600 |
| Gloria | F | US | +1 (305) 555-1500 |
| Gloria | F | US | +1 (305) 555-1600 |
| James | M | US | +1 (305) 555-1500 |
| James | M | US | +1 (305) 555-1600 |

## 练习

# 级别 1

10. 使用 `IN=` 选项合并

- a. 获取初始程序 `p110e10`。
- b. 在 `PROC SORT` 步骤之后添加一个 `DATA` 步骤，通过 `Supplier_ID` 合并 `Work.product` 和 `orion.supplier`，创建一个名为 `Work.prodsup` 的新数据集。
- c. 提交程序并确认创建了 `Work.prodsup`，且包含 556 个观测值和 10 个变量。
- d. 修改 `DATA` 步骤，仅输出位于 `Work.product` 但不在 `orion.supplier` 中的观测值。需要添加一个引用 `MERGE` 语句中 `IN=` 变量的子集 `IF` 语句。
