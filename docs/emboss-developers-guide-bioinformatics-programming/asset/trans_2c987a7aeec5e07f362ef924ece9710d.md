

- 每个 FI 文件下的 FC 记录用于测试正确的行数，或 FZ 记录用于测试文件大小
- 每个 FI 记录下的一个或多个 FP 测试用于测试文件内容
- 一个或多个 DI 记录用于其被使用的输出子目录
- 一个 RQ 记录用于所需应用程序的名称（如果有的话）
- 应为 stderr 和 stdout 中的每一个提供 FI、FZ（或 FC）和 FP 记录

## 7.2.2.1 测试数据的位置

任何测试数据，即应用程序所需的输入文件，都应添加到目录：

```
emboss/test/data
```

如果需要许多输入文件，为了保持整洁，可以将它们放在上述目录的子目录下。无论哪种情况，都不应不必要地创建文件：很可能，emboss/test/data 下已经存在一个适合您需求的文件。有关此目录内容的更多信息将在下文介绍（第 7.2.4 节，*有用的文件和目录*）。

## 7.2.3 运行应用程序质量保证测试

要执行测试，必须编辑您的 .embossrc 文件（在您的主目录中）或 emboss.default 文件，以将 EMBOSS 环境变量 emboss_qadata 设置为测试目录，例如：

```
/home/auser/emboss/emboss/test
```

要运行测试，必须运行脚本：

```
/emboss/scripts/qatest.pl
```

从目录 /emboss/test/qa 运行。命令的形式如下：

```
qatest.pl TestIdentifier
```

其中 TestIdentifier 是 qatest.dat 中相应条目的 ID 记录上给出的测试标识符。

### 7.2.3.1 示例测试

假设您想运行先前在 qatest.dat 中显示的示例条目：

```
ID myprogram-ex
AB myemboss
AA myprogram
IN
FI stderr
FC = 2
FP 0 /Warning: /
FP 0 /Error: /
FP 0 /Died: /
FI P10932.myprogram
FC = 5
FP /^Usage: embl-id:P10932\n/
FP /^Length: 2167\n/
//
```

还假设您位于目录 emboss/test 中。要运行测试 myprogram-ex，您将键入：

```
cd qa
../../scripts/qatest.pl myprogram-ex -keep
```

如果测试完成后要保留输出文件，对于不包含 DL keep 记录的测试，则必须使用 -keep 限定符调用 qatest.pl。如果不这样做，输出文件将被删除。因此，如果测试包含以下行：

```
ID myprogram-keep
DL keep
```

则将这样调用它：

```
../../scripts/qatest.pl myprogram-ex
```

无论哪种情况，输出文件都将在主结果目录中创建。如果测试标识符行是

```
ID myprogram-ex
```

则结果目录将是：

```
emboss/qa/myprogram-ex
```

对于其他测试，文件也可能写入主结果目录中的子目录（请参阅 DI 和 DF 记录）。

如果在未在 qatest.dat 中定义的内容上运行 qatest.pl，它将报告：

```
Tests total: 0.
```

如果成功，除非测试条目包含 DL keep 行，或命令行上指定了 -keep，否则所有文件都将被删除。

如果失败，它将报告原因，并且所有结果都将保存在结果目录中以供检查。例如，您会检查 myprogram-ex，然后确定问题，更新测试定义，并重试直到成功。

典型会话如下所示：

```
../scripts/qatest.pl -without=srs
Tests total: 1586 pass: 1586 fail: 0
Skipped: 12 check: 1 embassy: 0 requirements: 11
Missing documentation html: 0 text: 0 sourceforge: 0
Time: 677 seconds
```

## 7.2.4 有用的文件和目录

在 /emboss/test/ 下存放了一些有用的文件。目录如下：

- **acd**: 测试应用程序的 ACD 文件。这些文件用于测试 ACD 文件解析。除非您扩展 ACD，否则不需要此目录。
- **data**: 已提及的测试数据目录。您的测试数据输入文件应放在此处，或放在其下的子目录中。
- **gb**: NBRF/GCG 数据库格式中的一些 GenBank 数据文件。
- **qa**: 必须从中运行所有测试的目录。应用程序输出文件写入其下方的各自结果目录，并在测试成功完成后删除，除非另有说明。
- **rc**: 此目录用于数据库和资源定义测试。您不需要它。
- **swnew**: 来自 SwissProt 数据库的文件，用于创建 tsw 测试数据库。
- **embl**: 来自 EMBL 数据库的文件，用于创建 tembl 测试数据库。
- **genbank**: 用于创建 tgenbank 测试数据库的一些 GenBank 数据文件。
- **memtest**: 用于跟踪内存泄漏的文件：您不需要此文件。
- **pir**: 来自 PIR 数据库的数据文件，用于创建 tpir 测试数据库。
- **swiss**: 来自 SwissProt 数据库的数据文件。
- **wormpep**: 来自 WormPep（蠕虫肽）数据库的数据文件。

## 8.1 简介

此处的准则描述了如何编写符合在线使用的 EMBOSS 风格的新应用程序文档：

```
http://emboss.open-bio.org/rel/dev/apps/
```

它们还涵盖 EMBASSY 包的文档：

```
http://emboss.open-bio.org/rel/dev/apps/EMBASSYPackagesTable.html
```

要了解文档情况，例如，请查看 seqret 应用程序的文档：

```
http://emboss.open-bio.org/rel/dev/apps/seqret.html
```

以及 HMMER 包的文档：

```
http://emboss.open-bio.org/rel/dev/apps/hmmer.html
```

您会注意到，应用程序和包文档被组织成各个部分，以便于导航。下文将解释各个部分以及生成文档的流程。

## 8.2 应用程序文档

### 8.2.1 ACD 文件文档

应用程序 ACD 文件（请参见第 5 章，C 编程）不需要显式文档，但在某些情况下，添加注释会很有帮助。注释行以 # 开头并持续到行尾（请参见第 4.1 节，*ACD 文件开发简介*）。

ACD 文件包括描述应用程序本身的应用程序定义，以及描述参数的一个或多个数据定义。定义具有详细描述应用程序或参数的属性。数据定义在文件中组织为“输入”、“输出”等部分。在生成应用程序文档时，会解析 ACD 文件。使用的组件包括：

- 应用程序名称（来自应用程序定义）和简短描述（来自应用程序定义的 `documentation:` 属性）
- 示例数据文件（来自“输入”部分）
- 命令行概要
- 应用程序选项表（来自数据定义）
- 相关应用程序链接列表（来自应用程序定义的 `groups:` 属性）。

因此，您应使用为此目的提供的实用程序来确保应用程序 ACD 文件有效且格式正确。

### 8.2.1.1 应用程序质量保证测试

应用程序 QA 测试的命令行会话包含在应用程序文档中。因此，您应在记录应用程序之前编写并运行这些测试（请参见第 7.2 节，*应用程序质量保证*），以确保示例文件能够正确生成。

如果您在记录应用程序之前未编写 QA 测试，请重新运行 `autodoc.pl`，它将创建其余三个包含文件（用法示例以及输入和输出文件），完整的 HTML 文档将创建在 `embassy/myemboss/emboss_doc/html/myprogram.html`

### 8.2.2 应用程序文档的各个部分

应用程序文档中的各个部分在下表中描述。

### 8.2.3 应用程序文档生成流程

生成应用程序文档的流程结合了手动编写的组件和自动生成的部分（主要来自解析 ACD 文件和 QA 测试）。该流程在很大程度上是自动化的，涉及运行 `autodoc.pl` 脚本，该脚本生成一个部分完成的*应用程序模板*，您需要手动完成它。

应用程序名称和索引术语直接写入应用程序模板。但是，大部分自动生成的内容保存在*包含文件*中，这些文件从模板 XML 包含文件生成。

`autodoc.pl` 包含在 EMBOSS 发行版的 `scripts` 目录下，例如：

```
/home/auser/emboss/emboss/scripts/autodoc.pl
```

