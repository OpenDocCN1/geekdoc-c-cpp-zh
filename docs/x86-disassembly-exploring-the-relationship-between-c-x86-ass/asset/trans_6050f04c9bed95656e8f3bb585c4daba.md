
# Windows 可执行文件

索引 `FirstThunk` 和 `OriginalFirstThunk` 数组。该 `OriginalFirstThunk` 用于标识需要解析的导入的 `IMAGE_IMPORT_BY_NAME` 结构，而 `FirstThunk` 是另一个需要解析的条目的索引。此过程持续持续直到 `FirstThunk` 的值为 -1，表示没有更多需要导入的转发值。

## 5.10 资源

### 5.10.1 资源结构

资源是模块中的数据项，使用所选编程语言很难存储或描述。这需要一个单独的编译器或资源生成器，允许插入对话框、图标、菜单、图像以及其他类型的资源（包括任意的二进制数据）。然后可以使用若干 API 调用从模块中检索资源。资源数据的基指向数据中的 `IMAGE_DIRECTORY_ENTRY` 条目，在该位置有一个 `IMAGE_RESOURCE_DIRECTORY` 结构：

```c
struct IMAGE_RESOURCE_DIRECTORY
{
    long Characteristics;
    long DateStamp;
    short MajorVersion;
    short MinorVersion;
    short NumberOfNamedEntries;
    short NumberOfIdEntries;
}
```

`Characteristics` 未被使用，`DateStamp` 通常是创建时间，尽管设置与否并不重要。`MajorVersion` 和 `MinorVersion` 与资源的版本信息有关：这些字段没有定义值。紧随 `IMAGE_RESOURCE_DIRECTORY_ENTRY` 之后，其数量由 `NumberNamedEntries` 和 `NumberOfIdEntries` 的总和定义。这些条目的的第一部分用于命名资源，后半部分用于 ID 资源，取决于 `IMAGE_RESOURCE_DIRECTORY` 结构中的值。资源结构的实际形状如下：

```c
struct IMAGE_RESOURCE_DIRECTORY_ENTRY
{
    long NameId;
    long *Data;
}
```

`NameId` 具有双重用途：如果最高位（或符号位）为 0，则低 16 位是资源的 ID 编号。或者，如果最高位被置，则这 31 位构成了从资源数据开始到该特定资源名称字符串的偏移量。`Data` 值也具有双重用途：如果最高位被置，则剩余的 31 位形成从资源数据开始到另一个 `IMAGE_RESOURCE_DIRECTORY` 的偏移量（即该条目是资源树的内部节点）。否则，这是一个叶子节点，`Data` 包含从资源数据开始到描述资源数据本身细节的结构的偏移量（可以被视为有序字节流）；

```c
struct IMAGE_RESOURCE_DATA_ENTRY
{
  long *Data;
  long Size;
  long CodePage;
  long Reserved;
}
```

`Data` 值包含指向实际资源数据的 RVA，`Size` 自言易懂，`CodePage` 包含用于解码资源中 Unicode 编码字符串的 Unicode 编码页（如果有的话）。`Reserved` 应被设置为 0。

## 5.10.2 布局

上述资源目录条目系统允许通过名称或 ID 编号简单存储资源。然而，这会很快变得复杂。不同类型的资源、资源本身以及其他语言中的资源实例可能会在资源资源目录中混在一起。由于这个原因，资源目录被赋予了一个工作结构，允许将不同的资源分开。

为了实现这一目的，资源条目的 'Data' 值指向另一个 `IMAGE_RESOURCE_DIRECTORY`，形成了一种类似于树形图的资源组织。第一层资源条目标识资源类型：光标、位图、图标及类似。它们使用 ID 方法来标识资源条目，总共有两个定义值。可以添加更多用户定义的资源类型。这些资源条目中的每一个都指向一个资源目录，命名资源本身。这些可以是任何名称或值。它们又指向另一个资源目录，该目录使用 ID 编号区分语言，允许为使用不同语言的系统提供不同的特定资源。最后，语言目录中的条目实际上提供了资源数据本身的偏移量，其格式未由 PE 规范定义，可以被视为任意字节流。

## 5.11 重定位

## 5.12 备绑定导入结构

## 5.13 Windows DLL 文件

Windows DLL 文件是 PE 文件的一种类型，但有几个关键区别：

- .DLL 文件扩展名
- `DLLMain()` 入口点，而不是 `WinMain()` 或 `main()`。
- PE 头中设置了 DLL 标志。

DLL 可以通过两种方式之一加载：a) 在加载时，b) 通过调用 `LoadModule()` Win32 API 函数。

### 5.13.1 函数导出

函数使用以下语法从 DLL 文件导出：

```c
__declspec(dllexport) void myFunction()...
```

- 这里的 *declspec* 关键字不是 C 语言标准，但被许多编译器实现以扩展函数和变量的特定选项。Microsoft C 编译器和运行在 Windows 上的 GCC 版本允许 `__declspec` 关键字和 `dllexport` 选项。

函数也可以从普通的 .exe 文件导出，带有导出函数的 .exe 文件可以类似于 .dll 文件的方式被动态调用。然而，这种情况很少见。

### 5.13.2 识别 DLL 导出

有几种方法可以确定 DLL 导出了哪些函数。本书将使用的（通常是隐式的）方法是 **dumpbin** 以下：

```
dumpbin /EXPORTS <dll file>
```

有几种方法可以确定 DLL 导出了哪些函数。本书将使用的（通常是隐式的）方法是 **dumpbin**：

```
dumpbin /EXPORTS <dll file>
```

有几种方法可以确定 DLL 导出了哪些函数。本书将使用的（通常是隐式的）方法是 **dumpbin**：

```
dumpbin /EXPORTS <dll file>
```

等等，让我重新评估 OCR 文本。OCR 文本有很多重复和损坏部分。我将根据提供的逻辑流清理它并合并页面。

修正后的文本逻辑：
1. "a import" -> "an import"
2. "needs resolved" -> "needs to be resolved"
3. "IMAGE_RESOURCE_DIRECTORY_ENTRY's" -> "IMAGE_RESOURCE_DIRECTORY_ENTRYs"（或保持不变）
4. 删除 [PAGE 57], [PAGE 58], [PAGE 59]。

让我们重新生成最终输出。
