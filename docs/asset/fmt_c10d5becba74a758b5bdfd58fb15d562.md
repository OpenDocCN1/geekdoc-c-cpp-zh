
# 第 4 章] 多重数据结构 71

在寻址过程中，并不是所有收到信的人都寄回了回执卡。营销经理是个多疑的人，他认为他的员工可能偷取了某些未发出的信件的回执卡，并寄回了这些卡片，以便他们从优惠中获利。

发出的信件已记录在一个文件中；每封发出的信有一条记录，包含信件号和其他与我们无关的信息。回执卡是机器可读的，并已复制到磁带上；每张寄回的回执卡都会产生一条记录，包含信件号和其他同样与我们无关的信息。信件文件和回执文件都按信件号顺序进行了排序。

需要一个程序来报告优惠的当前状态。报告的每行对应一个信件号；共有四种行，每行都包含信件号、一个代码和一个消息。这四种行是：

- `NNNNN 1` 已发送信件并收到回执
- `NNNNN 2` 已发送信件，未收到回执
- `NNNNN 3` 未发送信件，收到回执
- `NNNNN 4` 未发送信件，未收到回执

有三个文件需要处理：信件文件、回执文件和报告文件。数据结构如下：

| `LFILE` | `RFILE` | `REPORT` |
|---|---|---|
| `LREC*` | `RREC*` | `LINE*` |
| | | |
| `TYPE 1°` | `TYPE 2°` | `TYPE 3°` | `TYPE 4°` |

在顶层存在完美的对应关系：程序每次运行时，它都会处理一个 `LFILE` 和一个 `RFILE` 并产生一个 `REPORT`。但在下一层没有这种对应关系。给定的信件号可能出现在 `LFILE` 和 `RFILE` 中，可能出现在其中之一，也可能两个都不出现。

我们可以通过各种方式详细说明输入文件结构，以获得我们需要的对应关系。例如，我们可以区分匹配记录和未匹配记录，如下：

![](img/2af52882003b66fe0217f904c606a0f9_87_0.png)

或者我们可以区分实际记录和缺失记录，如下：

![](img/2af52882003b66fe0217f904c606a0f9_87_1.png)

或者我们可以同时使用这两种区分，如下：

![](img/2af52882003b66fe0217f904c606a0f9_87_2.png)

# 第 4 章] 多重数据结构 73

`RFILE` 也可以画出类似的结构。然而，无论我们做些什么来实现对应关系，我们都无法避免两个约束：

- 如果不引用另一个文件，程序无法正确解释 `LFILE` 或 `RFILE`
- 程序结构中不能包含一个 `process lrec` 的组件或一个 `process rrec` 的组件。

这两个约束都源于任何归并问题的本质：任何一个被归并的输入文件都无法孤立地解释；不能用一个唯一的程序来处理输入文件中的每条记录，因为根据其他文件中是否存在匹配记录，输入文件中的记录具有不同的含义。

选择最简单的数据结构，即在每个文件中区分匹配记录和未匹配记录，我们得到了以下对应关系：

`LFILE`、`RFILE` 和 `REPORT` 的对应关系为：

- `MATCHED LREC`、`MATCHED RREC` 和 `TYPE1` 对应；
- `UNMATCHED LREC` 对应 `TYPE2`；
- `UNMATCHED RREC` 对应 `TYPE3`；
- 输入文件中没有内容对应 `TYPE4`。

列出并分配可执行的操作是直观的，我们得到了以下程序：

```
PMAGIC seq

open LFILE; read LFILE;

open RFILE; read RFILE;
```

## 第4章] 多重数据结构 77

`01 N.`
`02 FILLER PIC X.`
`02 FILLER PIC X(8).`

我们可以将对 `N` 的赋值写为：

```
IF LKEY < RKEY

MOVE LKEY TO N

ELSE MOVE RKEY TO N.
```

选择的条件变为：

```
IF LKEY = N AND RKEY = N
```

以及

```
IF LKEY = N and RKEY NOT = N ...
```

循环体 `PMBODY` 的条件是：

```
UNTIL N NOT LESS THAN “E”...
```

这种解决方案避免了操作上的困难，并提供了一个高效且易于理解的程序。然而，通常会采用不同的解决方案：消除了变量 `N`，得到程序如下：

```
program

PMAGIC seq

open LFILE; read LFILE;

open RFILE; read RFILE;

PMBODY iter until EOF-L and EOF-R

PROCNUM select LNO = RNO

write type1;

read LFILE;

read RFILE;

PROCNUM or LNO < RNO

write type2;

read LFILE;

PROCNUM or LNO > RNO

write type3;

read RFILE;

PROCNUM end
PMBODY end
close LFILE:
close RFILE:
PMAGIC end
```

这个程序的可读性较差。`PMBODY` 是一个遍历一组键的迭代，但在每次执行 `PMBODY` 的迭代部分时，并没有一个变量来标识正在处理的键。例如，如果我们希望生成另一个包含已处理键键值的输出文件，我们就会陷入困境：我们要么需要重新引入 `N`，要么必须在 `PROCNUM` 的每个部分中插入代码。

## 4.4

排序程序的标准形式可能会因合并选择部分而发生扭曲：即没有使用相同的程序组件来处理两个或多个用例。

考虑问题 6 的第 2 个版本，其中付款文件必须与客户主文件进行排序。在消除了第四种匹配情况后，我们得到了右侧所示的程序结构。
