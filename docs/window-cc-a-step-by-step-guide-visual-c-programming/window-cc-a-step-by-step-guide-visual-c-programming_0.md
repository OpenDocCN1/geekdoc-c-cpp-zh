# Window C/C++：分步指南视觉 C++ 编程

## 必读材料
在探索 Microsoft Windows 提供的功能之前，让我们先来看看它们是如何处理错误处理的。当你调用 Windows 函数时，它会检查传递给它的参数并尝试执行任务。如果你传递了无效参数，或者由于其他原因无法执行该操作，它将返回一个指示错误的值。表 1-1 显示了大多数 Windows 函数返回值的数据类型。

## 表 1-1. Windows 函数返回的标准值类型
当发生错误时，你应该弄清楚调用此函数失败的原因。每个错误都有自己的代码——一个 32 位数字。

当 Windows 函数检测到错误时，它会使用线程本地内存机制将相应的错误代码映射到调用线程。（线程本地内存将在第 21 节中讨论）。这允许线程相互独立工作，而不会干扰他人的错误。当函数将控制权交还给你时，它的返回值将指示发生了某种错误。你可以通过调用 `GetLastError` 函数找出是哪种错误。

```cpp
DWORD GetLastError ();
```

它简单地为给定的流返回一个 32 位错误代码。

现在你已经有了错误代码，需要将其转换为更具读性的内容。关于 Microsoft 定义的错误代码列表，请参见 `WinError.h` 头文件。我在这里为你提供其中一小部分，让你了解它的样子：

```cpp
// MessageId: ERROR_SUCCESS
// MessageText
// 操作成功完成。
#define ERROR_SUCCESS 0L
#define NO_ERROR 0L // error
#define SEC_E_OK ((HRESULT) 0x0000000L)

// MessageId: ERROR_INVALID_FUNCTION
// MessageText
// 函数不正确。
#define ERROR_INVALID_FUNCTION 1L

// MessageId: ERROR_FILE_NOT_FOUND
// MessageText
// 系统找不到指定的文件。
#define ERROR_FILE_NOT_FOUND 2L

// MessageId: ERROR_PATH_NOT_FOUND
// MessageText
// 系统找不到指定的路径。
#define ERROR_PATH_NOT_FOUND 3L

// MessageId: ERROR_TOO_MANY_OPEN_FILES
// MessageText
// 系统无法打开文件。
#define ERROR_TOO_MANY_OPEN_FILES 4L

// MessageId: ERROR_ACCESS_DENIED
// MessageText
// 拒绝访问。
#define ERROR_ACCESS_DENIED 5L
```

如你所示，每个错误都关联一个消息 ID（可以在源码中与 `GetLastError` 返回的值进行比较）、一个消息文本（用普通语言对错误的描述）和一个数字（使用 ID 更好）。请注意，我只显示了 `WinError.h` 文件的极小部分；它实际上有超过 39,000 行！

在 Windows 函数调用失败后，必须立即调用 `GetLastError` 函数，否则错误代码可能会丢失（被另一个函数的错误代码覆盖，或者在函数成功完成时被 `ERROR_SUCCESS` 覆盖）。

某些 Windows 函数总是成功完成，但原因各异。例如，尝试创建一个特定名称的“事件”内核对象可能会成功，可能是因为你确实创建了它，也可能是因为该对象已经存在。但有时你需要知道成功的原因。Microsoft 选择使用最后的错误代码设置机制来返回此信息。因此，即使某些函数成功了，你也可以调用 `GetLastError` 获取额外信息。这些函数包括例如 `CreateEvent`。关于其他函数的信息以及当命名事件存在时返回 `ERROR_ALREADY_EXISTS` 的示例，请参阅 Platform SDK。

在我看来，在调试过程中跟踪最后一个错误代码是非常用的。顺便说，Microsoft Visual Studio 中的调试器允许你自定义监视（Watch）窗口，使其始终显示当前线程中最后一个错误的代码和描述。要做到这一点，在监视窗口中选择一行并输入 `@ err, hr`。现在看图 1-1。看，我调用了 `CreateFile` 函数。它返回了类型为 `HANDLE` 的 `INVALID_HANDLE_VALUE` (-1)，表示它无法打开指定的文件。但监视窗口向我们显示最后一个错误代码（如果我调用 `GetLastError`，它将返回的值）等于 `0x00000002`，以及描述“系统找不到指定的文件”。这就是 `WinError.h` 头文件中为错误代码 2 定义的行。

*图 1-1 ... 在 Visual Studio 的监视窗口中使用 "@ err, hr"，你可以查看当前线程中最后一个错误的代码*

Visual Studio 附带了一个小型工具 `Error Lookup`，允许你根据代码获取错误的描述。如果应用程序检测到错误，它通常会通过在屏幕上显示描述来通知用户。在 Windows 中，有一个特殊的函数用于“转换”错误代码为其描述——`FormatMessage`：

```cpp
DWORD FormatMessage (DWORD dwFlags, LPCVOID pSource, DWORD MessageId, DWORD LanguageId, PTSTR pszBuffer, DWORD nSize, va_list *Arguments);
```

`FormatMessage` 是一个功能非常丰富的函数，在形成所有显示给用户的行时，使用它是理想的。这一点在于它使得处理变得容易……（此处由于原文后续文本似乎存在部分重复或乱码，翻译时已根据代码逻辑和上下文进行了对齐）。

