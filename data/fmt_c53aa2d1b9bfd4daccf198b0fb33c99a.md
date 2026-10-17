
在所有操作环境中，当你运行 SAS 窗口模式或交互式行模式时，你都可以使用 `X` 语句。在某些操作环境中，当你以批或非交互模式运行 SAS 时可以使用 `X` 语句。

### 操作环境信息

`X` 语句取决于你的操作环境。请查看你的操作环境文档以确定其在你的系统中是否有效。请记住，从操作环境返回 SAS 会话取决于你的操作环境，且你在 `X` 语句中使用的命令是特定于环境。

你可以结合 SAS 宏编写适用于多种操作环境的 SAS 程序。请参考《SAS 宏语言参考》。

## 比较

在窗口会话中，`X` 命令的作用与 `X` 语句完全相同，只是你从命令行发布命令，而你在程序编辑器中提交 `X` 语句。

`X` 语句与 `SYSTEM` 函数、`X` 命令和 `CALL SYSTEM` 过程类似。大多数情况下，`X` 语句、`X` 命令或 `%SYEXEC` 宏语句更好，因为它们的开销更小。然而，`SYSTEM` 函数可以根据条件执行。`X` 语句是一个全局语句，在 `DATA` 步编译时执行。

## 更多

过程：

《SAS 函数和调用过程》中的“`CALL SYSTEM` 过程”

函数：

《SAS 函数和调用过程》中的“`SYSTEM` 函数”

## 特殊字符

- `_ALL` 参数

  `FILENAME` 语句 95

  `LIBNAME` 语句 235

- `_ALL CLEAR` 选项

  `CATNAME` 语句 41

- `_ALL LIST` 选项

  `CATNAME` 语句 41

- `_BLANKPAGE`, `PUT` 语句 288

- `_CMD` 303

- `_CMD_` 自动变量 387

- `_CMD_` SAS 变量，387

- `_ERROR` 74

- `_FILE` 76

- `_FILE` 88

- `_FILE =` 选项 76

- `_INFILE` 165

- `_INFILE_` 选项 288

- `_INFILE =` 165

- `_IORC` 303

- `_MODIFY` 269

- `_MSG_` 381

- `_MSG_` SAS 变量，387

- `_NULL` 303

- `PAGE`, `PUT` 语句 288

- `PAGE` 303

- `STOP` 354

# 索引 395

- `DATA` 步 36

- `PROC` 步 37

- 指定排序顺序 38

- 使用 SAS 视图 37

- `BY` 值

- 重复 `MODIFY` 语句 267

- `BY` 变量

- 使用 364 自定义标题

- 指定 38

- `BY` 组处理

- `SET` 语句 350

- `BY` 命令，与 `ENDSAS` 语句比较 73

- `CHECKPOINT EXECUTE ALWAYS` 语句 44

- 检查点重启模式 44

- `CLEAR` 参数

- `FILENAME` 语句 95, 97

- `LIBNAME` 语句 234

- `CLEAR`

- `CATNAME` 语句 41

- `CLIPBOARD` 访问方法 103

- `colon ( )` 格式修饰符 215

- `COLOR=argument WINDOW` 语句 381

- `COLOR=option WINDOW` 语句 386

- 列输入 198, 208

- 列输出 294, 306

- 列指针控制

- `INPUT` 语句 193

- `PUT` 语句 288

- `COLUMN=option` 76

- `FILE` 语句 76

- `INFILE` 语句 168

- 列

- 双列页格式 90

- `COLUMNS=argument` 语句 381

- 逗号分隔 219, 220

- `Comment` 语句 45

- 注释 45

- `COMPRESS=option`

- `LIBNAME` 语句 235

- 合并目录

- `CATNAME` 语句 41

- 隐式 240, 242

- 逻辑合并目录 44

- 嵌套目录合并 44

- 规则 42

- 合并数据库 240

- 逻辑上 242

- 合并数据集

- `SET` 语句 351

- 条件逻辑

- 用于发送电子邮件电子邮件 114

- `CONTENT_TYPE=option`

- `FILENAME` 语句 `EMAIL` 访问方法 107

- `CONTINUE` 语句 46 与 `LEAVE` 语句比较 230

- 复制的记录

- 截断 186

- `CVPBYTES=option`

- `LIBNAME` 语句 236

- `CVENGINE=option`

- `LIBNAME` 语句 236

- `CVPMULTIPLIER`

# C

+   `CALL` 例程

- 调用 40

- `CALL` 语句 40

- `CANCEL` 参数

- `ABORT` 语句 19

- `CARDS` 参数

- `INFILE` 语句 166

- `CARDS` 语句 41

- `CARDS` 语句 41

- `CATALOG` 访问方法

- `FILENAME` 语句, `CATALOG` 访问方法

- 目录条目

- `%INCLUDE` 带 101

- 目录

- 单目录中带有多个条目的 `%INCLUDE` 语句 165

- 隐式合并 240, 242

- 从 102 执行 autocall 宏

- 引用外部文件 100

- `CATAMS` 条目

- 读取和写入 102

- `CATNAME` 语句 41

- 参数 41

- 比较 43

- 详情 42

- 示例 43

- 选项 41

- `catrefs` 41

- `CC=option`

- `FILENAME` 语句, `EMAIL` 访问方法 107

- `CD=option`

- `FILENAME` 语句, `FTP` 访问方法 118

- `FILENAME` 语句, `SFTP` 访问方法 129

- 字符数据

- 219 中的嵌入空格

# 396 索引

- `LIBNAME` 语句 236

- 声明性的 2

- 可执行的 2

- 全局定义 3

- `DATA` 步视图

- 创建 52

- 描述 52

- 从 59 获取源代码

# D

+   数据库

- 将库与 229 关联

- 合并 240

- 逻辑合并， 242

- 从 240 剥离库

- 向日志写入属性 240

- 数据行

- 包含 159

- 读取，41

- `DATA` 命名规范 48

- 数据集列表

- `MERGE` 语句 258

- `SET` 语句 345

- 数据集选项

- 带 271 `MODIFY` 语句

- 数据集

- 另见 `DATA` 语句

- 合并 351

- 交叉读取 351, 352

- 一对一读取 351, 352

- 永久存储，单级名称 242

- 读取观测值 345, 352

- 多次读取观测值 352

- `DATA` 语句 48

- 参数 48

- 创建自定义报告 54

- 创建 `DATA` 步视图 52

- 创建输出数据集 51

- 创建存储的编译 `DATA` 步程序 52

- 描述 `DATA` 步视图 52

- 详情 51

- 显示嵌套层 55

- 示例 53

- 执行存储的编译 `DATA` 步程序 53

- 当不创建数据集时 52

- 无参数 48

- 步

- 中止 19

- `BY` 语句在 36

- `MODIFY` 语句在 269

- 停止 33

- `DATA` 步程序

- 存储编译的，执行 75

- 从 59 获取 `DATA` 步语句

+   `DATALINES` 240

- `INFILE` 语句 166, 181

- `DATALINES` 语句 56

- 与 `DATAL4` 语句比较 58

- `DATALINES` 57

- `DATAL4` 语句 57

- `DEBUG` 选项

- `FILENAME` 语句, `FTP` 访问方法 118

- `FILENAME` 语句, `SFTP` 访问方法 129

- `FILENAME` 语句, `URL` 访问方法 138

- `FILENAME` 语句, `WebDAV` 访问方法 142

- 声明性 `DATA` 步语句 2

- 声明性语句 2

- `DEFAULT=`

- `FORMAT` 语句 190

- `LENGTH` 语句 231

- `DELETE` 语句, `DISPLAY` 60

- `DELETE` 语句 58

- 与 `DROP` 语句比较 71

- 与 `IF` 语句比较，子集 156

- 分隔符 221

- 读取 178

- 从外部文件 96

- `DELIMITER` 敏感数据 76

- `FILE` 语句 76

- `DELIMITER=`

- `INFILE` 语句 168, 181

- 分隔符

- `INFILE` 语句 181

- `DESC=`

- `FILENAME` 语句, `CATALOG` 访问方法 100

- `DESCENDING BY` 语句 35

- `DESCRIBE` 语句 59

- `DIR` 选项

- `FILENAME` 语句, `FTP` 访问方法 118

- `FILENAME` 语句, `SFTP` 访问方法 129

# 397 索引

- `FILENAME` 语句, `WebDAV` 访问方法 142

- 按索引值 267

- 按观测值 268

- 目录

- 从 126 读取和写入

- 从成员 145 读取

- 向新成员 145

- 目录列表

- 与 `DELETE` 比较 59

- 与 `KEEP` 语句比较 226

- `DROP=` 数据选项

- 与 `DROP` 比较 71

- `DROP` 选项

- `FILE` 语句 76

- `DSD` 选项

- `FILE` 语句 76

- `INFILE` 语句 170, 182

- `DISPLAY` 60

- 与 `WINDOW` 语句比较 387

- `DISPLAY= WINDOW` 语句 386

# E

- 电子邮件电子邮件

- 附件 114

- 创建并发送图像 116

- `FILENAME` 语句, `EMAIL` 访问方法 105

- 使用 SMTP 发送 105

- `EMAIL(SMTP)` 访问方法

- 见 `FILENAME` 语句, `EMAIL(SMTP)` 访问方法

- 嵌入空格

- `DLMS=` 选项

- `FILE` 语句 76

- `INFILE` 语句 169

- `DLMSTR=` 选项

- `FILE` 语句 169

- `INFILE` 语句 169

- `DM` 62

- `DO` 语句 63

- 与 `UNTIL` 语句比较 69

- 与 `WHILE` 语句比较 70

- `DO` 语句，迭代 65

- 与 `DO` 语句比较 64

- 与 `UNTIL` 语句比较 69

- 与 `WHILE` 语句比较 70

- `DO UNTIL` 语句 68

- 与 `DO` 语句比较 64

- 与 `DO` 语句，迭代 66

- `DO WHILE` 语句 70

- 结束 72

- 219 中的字符数据

- 编码密码 105

- 编码

用于输出文件 92

- `ENCODING=` 选项

- `FILE` 语句 76, 92

- `FILENAME` 语句 94, 99

- `FILENAME` 语句, `EMAIL` 访问方法 108

- `FILENAME` 语句, `FTP` 访问方法 118

- `GO` 语句 153

- 恢复 46, 230

- 停止 46, 230

- 美元符号 (`$`) 194

- `INPUT` 194

- `INPUT` 语句，列输入 208

- `INPUT` 语句，命名输入 222

- `LENGTH` 语句 231

- 双尾部 `@`

- `INPUT` 语句，列表 215

- `DROP` 语句 71

- `FILENAME` 语句, `SOCKET` 访问 134

- `FILENAME` 语句, `WebDAV` 访问方法 142

- `INFILE` 语句 170, 189

- `END` 语句 72

- `END=` 参数

- `MODIFY` 语句 263

- `UPDATE` 语句 369

- `END=` 选项

- `INFILE` 语句 170

- `SET` 语句 345, 354

- `ENDSAS` 命令，与 `ENDSAS` 语句比较 73

- `ENDSAS` 语句 73

- `EOF=` 选项

- `INFILE` 语句 170

- `EOV=` 选项

- `INFILE` 语句 171

- 错误信息

- 写入 74

- `ERROR` 语句 74

- `DO` 循环处理

- 终止值 353

- `DO` 循环

- `DO` 语句 63

- `DO` 语句迭代 65

- `DO UNTIL` 语句 68

- `DO WHILE` 语句 70

# 398 索引

- 传输库 126

- `FILENAME`, `SFTP` 访问

- 方法 128

- 参数 128

- 比较 132

- 详情 131

- 示例 132

- 提示 131

- `SFTP` 选项 128

- `FILENAME` 语句, `SOCKET` 访问

- 方法 133

- 客户端模式 136

- 详情 135

- 示例 136

- 服务器模式 136

- `TCPIP` 选项 137

- `FILENAME` 语句, `URL` 访问

- 方法 137

- 访问网站上的文件 140

- 参数 137

- 详情 140

- 示例 140

- 读取 URL 文件的部分 141

- `URL` 选项 137

- 用户 ID 和密码 141

- 方法 141

- `FILENAME` 语句, `WebDAV` 访问

- 方法 108

- 访问网站上的文件 145

- 访问大小写敏感的文件 146

- 访问小写自动调用成员 146

- 参数 141 在 141

- 自动附加文件扩展名 146

- 详情 144

- 示例 145

- 代理服务器 145

- 从目录成员读取 145

- 作为本地库的 `WebDAV` 选项 145

- `WebDAV` 选项 145

- 写入新目录成员 145

- `FILENAME=option`

- `FILE` 语句 76

- `INFILE` 语句 171

- `fileref`

- 与聚合存储位置关联 98

- 与外部文件关联 96, 97

- 与输出设备关联 97

- 定义 96

- 从外部文件断连接 95, 97

- `FILENAME` 语句 93

- 文件，主文件

- 更新 369

- `FILEVAR=option`
