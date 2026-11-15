

| 章节 | 描述 | 生成方式 |
|---|---|---|
| Name | 应用程序名称、简短描述和版本号。 | 从应用程序 C 源代码和 ACD 文件自动生成。 |
| Function | 对应用程序输入、输出和功能的简洁、正式描述。 | 由应用程序作者编写。 |
| Description | 适合生物学最终用户的应用程序描述。 | 由应用程序作者编写。 |
| Command line arguments | 如何在命令行中使用应用程序的概要，包括命令行概要和参数表。 | 自动生成。 |
| Usage | 用法示例，即命令行会话，或例如 wEMBOSS、Jemboss 或 SOAPLAB 中的等效内容。 | 从质量保证测试用例自动生成。 |
| Input Files | 示例输入文件。可选的输入文件描述（例如文件格式）或指向同一文件的 URL。 | 示例输入文件从测试用例自动生成。描述由应用程序作者编写。 |
| Data Files | 数据文件示例。可选的数据文件描述（例如文件格式）或指向同一文件的 URL。 | 示例数据文件从 ACD 文件自动生成。描述由应用程序作者编写。 |
| Output Files | 示例输出文件。可选的输出文件描述（例如文件格式）或指向同一文件的 URL。 | 示例输出文件从测试用例自动生成。描述由应用程序作者编写。 |
| Algorithm | 适合计算机科学家的算法技术描述。 | 由应用程序作者编写。 |
| Notes | 外围文档，例如使用说明。 | 由应用程序作者编写。 |
| Warnings | 谨慎的使用建议、已知错误等。 | 由应用程序作者编写。应用程序特定的消息可以通过搜索代码找到。 |
| Diagnostics | 应用程序可能生成的诊断警告和错误消息。 | 由应用程序作者编写。应用程序特定的消息可以通过搜索代码找到。 |
| Authors | 作者联系信息。 | 从源代码自动生成。 |
| Revision History | 应用程序修订历史，包括上次修订日期、修订作者姓名和关于修订的简要说明。 | 用于主要修订。EMBOSS 代码的详细历史记录可在 CVS 中查找。 |
| References | 文献参考和如何引用应用程序的说明。 | 如何引用 EMBOSS 的说明会自动包含。否则，由应用程序作者编写。 |
| See Also | 同一组中应用程序的链接列表。 | 从 ACD 文件自动生成。 |
| Target Users | 应用程序面向的用户群（例如生物学家、生物信息学家、系统管理员等）。 | 由应用程序作者编写。 |
| Exit Status | 应用程序退出时可能返回给操作系统的值。 | 从源代码自动生成。 |

要记录一个新程序，首先确保你有一组最新的已编译程序，并且你编写但不属于主 EMBOSS 包的任何程序都已删除其可执行文件。否则，对它们的引用可能出现在自动生成的 "See Also" 部分中（见上文）。ACD 文件应完整且经过验证，并且应用程序的 QA 测试应已运行。

要生成文档，请依次对要记录的每个应用程序运行 autodoc.pl。

对于 EMBOSS 应用程序：

```
autodoc.pl ApplicationName
```

对于 EMBASSY 应用程序：

```
autodoc.pl -embassy=PackageName ApplicationName
```

应将 PackageName 和 ApplicationName 替换为合适的名称。以下示例假设你正在 EMBASSY 包 myemboss 中工作，并编写名为 myprogram 的程序。要记录该应用程序：

- 1. 移动到文档目录：

```
cd embassy/myemboss/emboss_doc/master
```

- 2. emboss_doc/master 目录中有一个用于记录 myemboss 应用程序的模板文件。将应用程序模板复制到同一目录下名为 myprogram.html 的文件：

```
cp template.html.save myprogram.html
```

- 3. 编辑此文件，将 'ProgramNameToBeReplaced' 替换为应用程序名称。这为文档的自动生成元素定义了命名的包含文件。

- 4. 运行 autodoc.pl：

```
autodoc.pl -embassy=myemboss myprogram
```

- 5. 在指定位置（见下文）编写文档文本以完成 myprogram.html。

该脚本将运行 wossname 以检查 myprogram 是否确实存在，然后生成带有包含指令的应用程序模板文档文件（供你填写），以及以下部分的包含文件：

- Name（整个部分）
- Synopsis（整个部分）
- Data Files（数据文件示例）
- Authors（整个部分）
- Revision History（整个部分）
- References（仅关于如何引用 EMBOSS 的说明）。

以下部分的包含文件是通过运行 QA 测试生成的，这就是为什么（通常）应在记录应用程序之前编写 QA 测试：

- Usage（整个部分）
- Input Files（仅输入文件示例）
- Output Files（仅输出文件示例）。

应用程序模板中的应用程序名称和索引术语也已正确设置。完成所有操作后，HTML 应用程序模板将创建在：

```
embassy/myemboss/emboss_doc/html/myprogram.html
```

要完成应用程序模板 myprogram.html，请按以下方式添加文档文本：

- 1. 编写 "Function" 部分。
- 2. 在 "Input Files" 部分编写输入文件描述（可选）。
- 3. 在 "Data Files" 部分编写数据文件描述（可选）。
- 4. 在 "Output Files" 部分编写输出文件描述（可选）。
- 5. 在 "Description" 部分编写应用程序描述。
- 6. 在 "Algorithm" 部分编写算法描述。
- 7. 在 "Notes" 部分编写外围文档。
- 8. 在 "Warnings" 部分编写使用建议、已知错误等。
- 9. 在 "Diagnostics" 部分编写警告和错误消息。
- 10. 在 "References" 部分编写参考文献（如适用）。

模板中已包含足够的注释，供你了解如何填写。

autodoc.pl 还生成纯文本格式的文档（包含所有包含文件中的文本），用于手册页，并在运行以下命令时显示：

```
application_name -help
```

完成模板并保存后，文档（HTML 和纯文本格式，以及包含文件）即可提交给 EMBOSS 作者以供在线发布。引用新文档的其他在线文件（例如应用程序索引 http://emboss.open-bio.org/rel/dev/apps/）将自动更新。

## 8.2.3.1 不使用 myemboss 时记录应用程序

记录 EMBOSS 应用程序时，请在以下目录中工作：

```
doc/programs/master/emboss/apps/
```

从 autodoc.pl 命令行中省略 -embassy=myemboss 限定符：

```
autodoc.pl ApplicationName
```

最终文档将写入：

```
doc/programs/html/myprogram.html
```

## 8.2.3.2 示例

以下示例适用于 seqret。所有路径均相对于文档目录，例如 /home/auser/emboss/emboss/doc/。

带有包含指令的应用程序模板文件为：

```
./programs/master/emboss/apps/seqret.html
```

## autodoc.pl 生成的文件

包含文件如下。所有文件均写入 /programs/master/inc/：

| 文件 | 描述 |
|---|---|
| ../secret.itable | 通过运行 acdtable 生成 |
| ../secret.ione | 由 autodoc.pl 从 ACD 文件生成 |
| ../secret.ihelp | 由 autodoc.pl 从 ACD 文件生成 |
| ../secret.itable | 由 autodoc.pl 从 ACD 文件生成 |
| ../secret.isee | 由 autodoc.pl 使用 ACD 文件中的组从 seealso 生成 |
| ../secret.usage | 从 QA 测试生成（使用 UsageExampleTemplate.xml） |
| ../secret.input | 从 QA 测试生成（使用 InputFilesTemplate.xml） |
| ../secret.output | 从 QA 测试生成（使用 OutputFilesTemplate.xml） |
| ../secret.comment | 由 autodoc.pl 生成，供手动编辑 |
| ../secret.history | 由 autodoc.pl 生成，供手动编辑 |

autodoc.pl 生成用于在线的最终 HTML 文件，包含所有数据：

```
./programs/html/secret.html
```

autodoc.pl 还编写一个纯文本文档文件，包含与完成的应用程序模板中完全相同的文档，但包含所有包含的文本：

```
./programs/text/secret.txt
```

## 8.3 EMBASSY 包文档

### 8.3.1 EMBASSY 包文档的章节

EMBASSY 包文档中的章节在下表中描述。

### 8.3.2 EMBASSY 包文档过程

生成 EMBASSY 包文档的过程与应用程序类似。手动编写的组件与自动生成的文本相结合。该过程再次涉及运行 autodoc.pl 脚本，该脚本生成一个部分完成的包模板，你需要手动完成它。

要记录一个新包，首先确保你有一组最新的已编译程序。要生成文档，请对包运行 autodoc.pl：

```
autodoc.pl PackageName
```

