

### 另请参阅

Rosenbloom 和 Lafler (2011c) 在将不同的宏赋值给 KEYS 时使用了 SUBMIT 而不是 GSUBMIT。

## 14.5 使用 SAS 编写和发送电子邮件

在程序处理期间或之后，你可以使用 SAS 生成电子邮件。这些可以是错误条件或程序成功终止的通知。电子邮件甚至可以包含附件。这个简单的示例将帮助你入门。阅读“另请参阅”中的参考文献，了解该技术的改进细节。

```sas
options emailsys=SMTP emailid="sam@caloxy.com"
        emailhost="caloxy.com" EMAILPORT=25;

* Define the fileref with the email engine;
FILENAME genmail email
        subject="Patient 205 ConMeds"
        to      = "Fred@caloxy.com"
        from    = "Sam@caloxy.com"
        attach  = "&path\\results\\E14_5.pdf";

ods pdf file="&path\\results\\e14_5.pdf"
        style=journal2;
proc print data=advrptv.connected
        (where=(subject='205'));
    id subject;
    var medstdt medspdt drug;
run;

ods pdf close;

data _null_;
    file genmail;
    put "Here are the ConMeds for Subject 205";
run;
```

- 1. 此电子邮件 ID 的邮件服务器属性在 options 语句中指定。这些选项也可以在配置文件中指定。EMAILID= 和 EMAILHOST= 选项将使用特定于你的邮件服务器的值。
- 2. 使用 FILENAME 语句定义电子邮件文件引用（GENMAIL）。注意 EMAIL 引擎的使用。
- 3. SUBJECT= 选项定义主题行。
- 4. 收件人的电子邮件地址使用 TO= 选项指定。
- 5. FROM= 选项指定发件人的电子邮件。这通常与 EMAILID 匹配。
- 6. ATTACH= 选项指定要附加的文件。
- 7. 生成要附加的文件。
- 8. 使用 data _NULL_ 步生成电子邮件正文。当 DATA 步编译时，开始生成电子邮件的过程就会发生。DATA 步中语句的条件执行可以更改电子邮件正文，但请记住，如果 DATA 步被编译，就会生成一封电子邮件。
- 9. FILE 语句指向使用 EMAIL 引擎生成的文件引用（GENMAIL）。
- 10. 电子邮件的文本使用 PUT 语句生成。

### 另请参阅

关于使用 SAS 通过电子邮件发送结果，已有不少论文。Hunley (2010) 提供了许多扩展示例，包括关于短信的讨论。Whitworth (2010) 有一个示例，涉及在发送电子邮件之前压缩文件。Rosenbloom 和 Lafler (2011d) 提供了一个简短的电子邮件示例。

SAS Jedi（Mark Jordan）写了几篇关于使用 SAS 以电子邮件发送文档的博客：http://blogs.sas.com/sastraining/index.php?/archives/81-Jedi-SAS-Tricks-Email-from-the-Front-Part-2.html。他还在 YouTube 上创建了一个相关视频：http://www.youtube.com/watch?v=qPobPZg2osc&feature=related。

SAS 论坛的两个帖子包含了对电子邮件使用的讨论：http://communities.sas.com/thread/10467 和 http://communities.sas.com/thread/11086。

## 14.6 获取物理位置信息

在 WINDOWS 操作系统下，你可以使用多种技术，利用 SAS 可用的信息来查找数据集或文件的物理位置。

### 另请参阅

Carpenter (2008b) 更详细地讨论了这些和其他技术。

### 14.6.1 使用 PATHNAME 函数

PATHNAME 函数返回给定 *文件引用* 或 *库引用* 的物理路径。尽管在 DATA 步中很少使用，但它已被证明在宏语言中非常宝贵。很多时候，即使我们知道 *库引用* 或 *文件引用*，也不一定知道物理路径。在此处，物理路径被加载到一个宏变量中，并在 LOG 中显示。

```sas
filename saspgm "&path\\sascode\\e14_6.sas";

%let pgmpath = %sysfunc(pathname(saspgm));
%put &pgmpath;
```

```text
C:\InnovativeTechniques\sascode\e14_6.sas
```

你甚至可以将其用于串联的 *文件引用*，例如自动调用库。要收集 SASAUTOS *文件引用* 中所有位置的当前位置，你可以指定：

```sas
%sysfunc(pathname(sasautos))
```

### 更多信息

第 13.8.2 节中的一个示例使用 PATHNAME 函数获取了一些位置信息。

### 14.6.2 SASHELP 视图和 DICTIONARY 表

现有 *库引用* 和 *文件引用* 的路径信息可以通过查看 SASHELP 视图和 SQL DICTIONARY 表来收集。在这里，你不仅可以找到 PATHNAME 函数返回的路径，还可以找到其他内容，如 ENGINE。

### SASHELP.VLIBNAM 和 DICTIONARY.LIBNAMES

视图 SASHELP.VLIBNAM（注意拼写）中的每一行都包含每个 *库引用* 的 *库引用* 和路径信息（对于串联的 *库引用*，有不止一行）。列表的一部分

环境变量的值可通过使用 %SYSGET 宏函数来访问。返回的值然后可以被加载到宏变量中，或者像这里所做的那样直接写入 LOG。

```sas
%put %sysget(SAS_EXECFILENAME);
```

E14_6.sas

当你想要不带 SAS 扩展名的程序名时，可以使用 %SCAN 或 %QSCAN 函数轻松地将其去除。

```sas
%put %qscan(%sysget(SAS_EXECFILENAME),1,.);
```

E14_6

当我们不仅需要知道 SAS 程序的名称，还需要知道其位置时（从增强编辑器执行时，这是正在执行的程序被检索到的位置），我们可以使用 SAS_EXECFILEPATH 环境变量。这里，该值由宏 %GRABPATHNAME 检索，然后写入 LOG。

```sas
%macro grabpathname;
   %sysget(SAS_EXECFILEPATH)
%mend grabpathname;

%put &grabpathname;
```

```text
114  %put &grabpathname;
C:\InnovativeTechniques\SASCode\Chapter14\E14_6.sas
```

### 14.6.4 获取 UNC（通用命名约定）路径

当程序驻留在网络服务器上时，服务器名称通常会映射到驱动器号。由于此驱动器号可以是用户特定的，因此知道程序位于 F:\ 驱动器上对某位用户来说并不一定对其他用户有帮助。正如使用所有先前方法所显示的，返回的总是映射驱动器；因此，需要一种不同的方法来获取实际的或 UNC 路径。虽然 UNC 路径信息并不存储在 SAS 可直接访问的位置，但仍然有可能获得此信息——只是过程更具挑战性。

当然，我们知道操作系统必须知道映射驱动器号与实际 UNC 位置之间的关系。在 Windows 下，此信息存储在动态链接库（DLL）中。Windows 有用于访问 DLL 中包含的信息的内部工具，并且可以在 SAS 中使用 CALL MODULE 例程来访问这些工具（也可以使用 MODULEN 和 MODULEC 函数）。要使这些工具可供 CALL MODULE 例程使用，我们必须首先创建一个 CATALOG SOURCE 条目，以使其运行。该条目包含传入和传出 Windows DLL 例程的参数，该例程用于获取 UNC 路径，名为 WNetGetConnectionA（请注意，此名称区分大小写）。

参数本身是每个例程所特有的。WNetGetConnectionA 例程需要三个参数。在此，SOURCE 条目已被写入 WORK 目录中的一个 catalog 中；但是，你通常会使它永久化，这样你只需运行此步骤一次。

```sas
filename sascbtbl catalog "work.temp.attrfile.source"; ❶

data _null_;
   file sascbtbl; ❷

   put "routine WNetGetConnectionA module=mpr minarg=3 maxarg=3 ❸ stackpop=called returns=long;";
   put "  arg 1 char input byaddr format=$cstr200.;";
   put "  arg 2 char update byaddr format=$cstr200.;";
   put "  arg 3 num update byaddr format=pib4.;";
run;
```

- ❶ 通过使用 DATA _NULL_ 步将 WNetGetConnectionA DLL 所需的属性写入一个 CATALOG SOURCE 条目来指定它们。文件引用必须是 SASCBTBL，并且必须指定 CATALOG 引擎。
- ❷ 例程属性使用 PUT 语句写入。DLL 名称区分大小写，必须完全按照所写指定。

然后可以使用 CALL MODULE 例程来访问 WNetGetConnectionA 例程并获取位置。

```sas
%macro grabdrive; ❺
  %qtrim(%qleft(%qscan(%sysget(SAS_EXECFILEPATH),1,\)))
%mend grabdrive;

%MACRO getUNC;
  %local dir path;
  %* Determine the UNC path for the SAS program being executed.;
  DATA _NULL_;
    length input_dir $200 output_dir $200;

    * The input directory drive letter: ONLY e.g. j: ;
    input_dir = "&grabdrive"; ❻
    output_dir = ;
    output_len = 200;
    call module("WNetGetConnectionA",
      input_dir, ❼
      output_dir,
      output_len);

    call symputx('dir',input_dir,'l'); ❽
    call symputx('path',output_dir,'l'); ❾
  RUN;

  %* Get the name for the program of execution.;
  %put drive letter is &dir; ❿
  %put path is &path; ⓫
  %put name is &grabpathname; ⓬
%MEND getunc;
```

- ❺ %GRABDRIVE 宏只返回驱动器号。
- ❻ %GRABDRIVE 宏获取带有冒号的映射驱动器号，例如 F:。这成为 DLL 的输入。第二个参数（OUTPUT_DIR）将包含返回的 UNC 路径。

