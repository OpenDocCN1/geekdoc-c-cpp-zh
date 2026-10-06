

http://doc.trolltech.com/4.3/qmake-manual.html.

.pro 文件的作用是列出项目中涉及的源文件。由于 qmake 用于构建 Qt 及其相关工具，Qt 能够很好地生成调用 moc、uic 和 rcc 的规则。因此，其语法非常简洁且易于学习。

项目文件的三种主要类型是 `app`（用于独立应用程序）、`lib`（用于静态和共享库）和 `subdirs`（用于递归子目录构建）。可以使用 `TEMPLATE` 变量来指定，如下：

```
TEMPLATE = lib
```

`subsdirs` 模板可用于构建子目录中的目标。在这种情况下，除了 `TEMPLATE = subsdirs` 之外，我们还需要指定 `SUBDIRS` 变量。在每个子目录中，qmake 会查找一个与目录同名的 `.pro` 文件并构建该项目。本书示例附带 `examples.pro` 文件使用 `subsdirs` 模板对各个示例运行 `qmake`。

如果没有 `TEMPLATE` 条目，默认是 `app`。对于 `app` 和 `lib` 项目，最常用的变量如下：

- `HEADERS` 指定项目的 C++ 头文件 (.h)。
- `SOURCES` 指定项目的 C++ 实现文件 (.cpp)。
- `FORMS` 指定要由 `uic` 处理的 Qt Designer .ui 文件。
- `RESOURCES` 指定要由 `rcc` 处理的 .qrc 文件。
- `DEFINES` 指定应该预定义的 C++ 预处理器符号。
- `INCLUDPATH` 指定 C++ 预处理器应该搜索的全局头文件目录。
- `LIBS` 指定要链接到项目的库。库可以使用绝对路径指定或使用受 Unix 启发的 `-L` 和 `-l` 标志指定（例如，`-L/usr/local/lib` 和 `-ldb_cxx`）。
- `CONFIG` 指定各种项目配置和编译器选项。
- `QT` 指定项目使用的 Qt 模块。（默认是 `core gui`，对应于 `QtCore` 和 `QtGui` 模块）。
- `VERSION` 指定目标库的版本号。

`TARGET` 指定目标可执行文件或库的基础名称，不包括任何扩展名、前缀或版本号。（默认是当前目录的名字。）

- `DESTDIR` 指定目标可执行文件应该存放的目录。（默认取决于平台；例如，在 Linux 上是当前目录，在 Windows 上是 debug/release 子目录。）

- `DLLDESTDIR` 指定目标库文件应该存放的目录。（它的默认值与 `DESTDIR` 相同。）

`CONFIG` 变量用于控制构建过程的各个方面。支持以下选项：

- `debug` 表示构建带有调试信息的可执行文件或库，并链接 Qt 库的调试版本。
- `release` 表示构建不带调试信息的可执行文件或库，并链接 Qt 库的发布版本。如果同时指定了 `debug` 和 `release`，则 `debug` 优先。
- `warn_off` 关闭尽可能多的警告。默认情况下，构建时是开启警告。
- `qt` 意味着应用程序或库使用了 Qt。此选项默认包含。
- `dll` 意味着构建一个共享库。
- `staticlib` 意味着构建一个静态库。
- `plugin` 意味着构建一个插件。插件总是共享库，因此此选项隐含 `dll` 选项。
- `console` 意味着应用程序需要向控制台写入内容（使用 `cerr`、`qWarning()` 等）。
- `app_bundle` 应用于 Mac OS X 构建，意味着可执行文件应该放在一个包（bundle）中，这是 Mac X 上的默认设置。
- `lib_bundle` 仅适用于 Mac OS X 构建，意味着库应该放在框架（framework）中。

要为名为 `hello.pro` 的项目文件生成 Makefile，我们输入：

```
qmake hello.pro
```

使用 `make nmake` 构建项目。我们也可以使用 `qmake` 生成 Visual Studio 项目 (.dsp)。

