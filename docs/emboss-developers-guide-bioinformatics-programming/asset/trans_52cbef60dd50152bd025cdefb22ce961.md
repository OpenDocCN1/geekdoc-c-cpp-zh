

## 9.5 质量保证测试

seqret 的质量保证测试定义在文件中：

```
.../emboss/emboss/test/qatest.dat
```

该应用程序的测试数据位于 /test 目录下，由输入文件、应用程序参数和相应的输出文件组成。

检查该文件可知，为该应用程序定义了许多测试，在各种输入条件下对其进行测试，以尽可能增强其鲁棒性。这些测试会频繁执行，以确保应用程序按宣传的方式工作，并且不会因（例如）库代码的最近更改而损坏。

质量保证测试（包括如何在 qatest.dat 中编写条目）在其他地方有详细介绍（第 7 章，质量保证）。

### Test 1

此测试从数据库中提取一个条目并将其写入文件：

```
ID seqret-ex1
UC Extract an entry from a database and write it to a file:
AP seqret
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_1.dat seqret-ex1
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 2

在屏幕上显示序列内容：

```
ID seqret-ex2
UC Display the contents of the sequence on the screen:
AP seqret
IN embl:x65923
IN stdout
FI stdout
FP /X65923/
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_2.dat seqret-ex2
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 3

使用限定词 -osformat 将结果以 GCG 格式写入：

```
ID seqret-ex3
UC Write the result in GCG format by using the qualifier '-osformat'.
AP seqret
CL -osf gcg
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.gcg
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_3.dat seqret-ex3
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 4

在命令行的输出 USA 中指定格式，将结果以 GCG 格式写入：

```
ID seqret-ex4
UC Write the result in GCG format by specifying the format
UC in the output USA on the command line.
AP seqret
CL -outseq gcg::x65923.gcg
IN embl:x65923
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.gcg
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_4.dat seqret-ex4
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 5

在提示符处的输出 USA 中指定格式，将结果以 GCG 格式写入：

```
ID seqret-ex5
UC Write the result in GCG format by specifying the format
UC in the output USA at the prompt.
AP seqret
IN embl:x65923
IN gcg::x65923.gcg
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.gcg
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_5.dat seqret-ex5
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 6

写入序列的反向互补：

```
ID seqret-ex6
UC Write the reverse-complement of a sequence:
AP seqret
CL -srev
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_6.dat seqret-ex6
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 7

提取位置从 5 开始到 25 结束之间的碱基：

```
ID seqret-ex7
UC Extract the bases between the positions starting at 5 and ending at 25:
AP seqret
CL -sbegin 5 -send 25
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_7.dat seqret-ex7
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 8

提取位置从 5 开始到序列结束前 5 个碱基处之间的碱基：

```
ID seqret-ex8
UC Extract the bases between the positions starting at 5
UC and ending at 5 bases before the end of the sequence:
AP seqret
CL -sbegin 5 -send -5
IN embl:x65923
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.fasta
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_8.dat seqret-ex8
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 9

读取 embl 数据库中所有以 h 开头的条目并将其写入文件：

```
ID seqret-ex9
UC Read all entries in the database 'embl' that start with 'h'
UC and write them to a file:
AP seqret
IN embl:h*
IN hall.seq
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI hall.seq
FP /H45989/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_9.dat seqret-ex9
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 10

此测试读取 embl 数据库中所有以 ab 开头的条目并将其写入文件。在此示例中，规范完全在命令行上完成。为了防止 UNIX 被 * 字符搞混，其前有一个反斜杠（\）：

```
ID seqret-ex10
UC Read all entries in the database 'embl' that start with 'ab'
UC and write them to a file.
UC In this example the specification is all done in the command line
UC and to stop Unix getting confused by the '*' character,
UC it has to have a backslash ('\\') before it:
AP seqret
CL 'embl:ab*' aball.seq
FI stderr
FC = 1
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI aball.seq
FP /^>AB000095/
FP 4 /^>/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_10.dat seqret-ex10
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

### Test 11

seqret 默认不读取特征，因为这会带来略微更快的性能。但是，如果您希望随序列一起读取特征并将其写出，则使用 -feature 将更改默认行为。请注意，输出文件使用 EMBL 格式。默认的 FASTA 格式将以 GFF 格式报告特征（文件 seqname.gff，其中 seqname 是输入序列的名称）：

```
ID seqret-ex11
UC seqret does not read in features by default because this results in
UC slightly faster performance. If however you wish to read in features
UC with your sequence and write them out on output, using '-feature' will
UC change the default behaviour to use any features present in the sequence.
UC N.B. use embl format for the output file as the default format 'fasta'
UC reports the features in gff (file "<seqname>.gff")
AP seqret
CL -feature
IN embl:x65923
IN embl::x65923.embl
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI x65923.embl
FP /X65923/
//
```

命令行会话如下：

```
% qatest.pl -simple -testfile=seqret_11.dat seqret-ex11
Tests total: 1 pass: 1 fail: 0
Time: 0 seconds
```

## 10.1 将应用程序纳入 EMBOSS 的好处

将第三方应用程序纳入 EMBOSS 有很多充分的理由，下面列举了其中几点。

- **分发** 显然，触达尽可能多的用户是可取的。EMBOSS 拥有数千名用户，许多网站会定期下载最新版本，因此任何纳入的软件都将被广泛分发。

- **培训成本** 纳入的软件的使用方式与所有其他 EMBOSS 应用程序完全相同。熟悉 EMBOSS 的人将能够使用任何已移植或封装的应用程序。当然，除了学习应用程序实现的特定方法之外，不需要额外的培训要求。无论应用程序是否在 EMBOSS 中，这都是一个要求。

- **支持成本** 纳入的应用程序将通过邮件列表获得 EMBOSS 提供的基本级别支持。支持级别取决于具体情况。对于已完全移植并理解将被 EMBOSS 采纳的应用程序，将获得全面支持。至少，用户对任何电子邮件查询都会得到回复，并被转发到可以获得更多帮助的地方。在应用程序的原作者已离开当前维护该应用程序的机构的情况下，这尤其有价值。

- **维护成本** 维护成本可能会有所节省。这同样取决于集成程度和具体安排。至少，EMBOSS 将调查任何错误并将相应报告转发给原始软件的作者。维护移植或封装以及原始代码会有额外成本，但这远远被收益所抵消。

