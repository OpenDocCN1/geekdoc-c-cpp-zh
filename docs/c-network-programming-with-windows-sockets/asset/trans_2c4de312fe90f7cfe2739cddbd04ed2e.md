
### 清单 8.1. USE.BAT 批处理文件。

```bat
@ECHO OFF
REM Replace PROJ with the actual project name

IF "%1"=="16" GOTO USE
IF "%1"=="32" GOTO USE

ECHO Directions for use: USE 16 or USE 32
GOTO END

:USE
IF NOT EXIST PROJ.%1 GOTO NOFILE
DEL *.APS
DEL *.BSC
DEL *.CLW
DEL *.EXE
DEL *.OBJ
DEL *.PCH
DEL *.PDB
DEL *.RES
DEL *.SBR
DEL *.VCW
DEL *.WSP
COPY PROJ.%1 PROJ.MAK
GOTO END

:NOFILE
ECHO %1-bit project file does not exist
GOTO END

:END
```

清单 8.2 中显示的批处理文件是一个脚本，用于将项目文件保存为相应的 16 位或 32 位 makefile。使用此批处理文件时要小心，因为您可能会不小心用 32 位版本覆盖 16 位 makefile，反之亦然。例如，不要运行 32 位 Visual C++、退出 Visual C++，然后运行 SAVE 16。这会导致您丢失 16 位项目文件。

### 清单 8.2. SAVE.BAT 批处理文件。

```bat
@ECHO OFF
REM Replace PROJ with the actual project name

IF "%1"=="16" GOTO USE
IF "%1"=="32" GOTO USE

ECHO Directions for use: SAVE 16 or SAVE 32
GOTO END

:USE
```

## WinSock TCP/IP 协议栈信息

此程序 WSINFO 允许您查看计算机正在运行的 WinSock TCP/IP 协议栈的详细信息。它使用以下 WinSock 函数：`WSAStartup()`、`WSACleanup()` 和 `WSAGetLastError()`。此程序是使用 Visual C++ 的 AppWizard 功能生成的，该功能会创建一个骨架应用程序，供您在此基础上构建。本书并非面向初学 Visual C++ 的程序员，因此只逐步讲解第一个示例程序。

生成此程序的第一步是使用 AppWizard 生成一个骨架应用程序。此应用程序使用单文档界面，而不是多文档界面。不需要任何特殊功能，例如工具栏、打印和打印预览、上下文相关帮助或对象链接和嵌入。与大多数应用程序相比，此应用程序非常简单。使用 WSINFO 作为项目名称。

在 AppWizard 完成其神奇工作后，编辑 WSINFO.H。此文件包含应用程序类 `CWSinfoApp` 的类声明。将以下可公开访问的成员变量添加到该类中：

```cpp
WSADATA m_wsaData;       // WinSock information
BOOL   m_bWinSockOK;     // TRUE if WinSock startup succeeded
int    m_nWinSockError;  // WinSock error code
```

`m_wsaData` 包含 `WSAStartup()` 返回的 WinSock 信息。如果 WinSock 启动成功，`m_bWinSockOK` 为 TRUE；否则为 FALSE。如果 WinSock 启动失败，`m_nWinSockError` 包含错误代码。WSINFO.H 文件也是包含 WINSOCK.H 头文件的好地方，因为 WINSOCK.H 会被包含在项目的其他源文件中。将 `ExitInstance()` 函数添加到该类中。此函数在应用程序退出时被调用，这为我们关闭 WinSock 提供了一个好机会。

此时，`CWSinfoApp` 类如下所示：

```cpp
class CWSinfoApp : public CWinApp
{
public:
    WSADATA m_wsaData;       // WinSock information
    BOOL   m_bWinSockOK;     // TRUE if WinSock startup succeeded
    int    m_nWinSockError;  // WinSock error code

public:
    CWSinfoApp();

    // Overrides
    virtual BOOL InitInstance();
    virtual int ExitInstance();

// Implementation

//{{AFX_MSG(CWSinfoApp)
    afx_msg void OnAppAbout();
//}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};
```

编辑 WSINFO.CPP 文件，以修改 `CWSinfoApp` 类的 `InitInstance()` 和 `ExitInstance()` 成员函数。在 `InitInstance()` 中，会调用 `WSAStartup()`。完成对 `InitInstance()` 的修改后，它如下所示：

```cpp
BOOL CWSinfoApp::InitInstance()
{
    // WinSock startup
    // If WSAStartup() is successful, we still
    // need to check the version numbers.

    WORD wVersionRequired = MAKEWORD(1, 1);  // WinSock 1.1 required
    m_bWinSockOK = FALSE;                    // not OK
    m_nWinSockError = 0;                     // no WinSock error
    if (WSAStartup(wVersionRequired, &m_wsaData) == 0)
    {
        if (wVersionRequired == m_wsaData.wVersion)
            m_bWinSockOK = TRUE;
        else
            WSACleanup();
    }
    else
        m_nWinSockError = WSAGetLastError();

    // Standard initialization
    // If you are not using these features and wish to reduce the size
    // of your final executable, you should remove from the following
    // the specific initialization routines you do not need.

    SetDialogBkColor();          // set dialog background color to gray
    LoadStdProfileSettings();    // Load standard INI file options (including MRU)

    // Register the application's document templates.  Document templates
    // serve as the connection between documents, frame windows and views.

    AddDocTemplate(new CSingleDocTemplate(IDR_MAINFRAME,
                RUNTIME_CLASS(CWSinfoDoc),
                RUNTIME_CLASS(CMainFrame),    // main SDI frame window
                RUNTIME_CLASS(CWSinfoView)));

    // create a new (empty) document
    OnFileNew();

    if (m_lpCmdLine[0] != '\0')
    {
        // TODO: add command line processing here
    }

    return TRUE;
}
```

在 `ExitInstance()` 中，会调用 `WSACleanup()`。完成对 `ExitInstance()` 的修改后，它如下所示：

```cpp
int CWSinfoApp::ExitInstance()
{
    // WinSock cleanup
    // If WinSock was started successfully, it must be shutdown.

    if (m_bWinSockOK)
        WSACleanup();

    // call the base class' member function

    return CWinApp::ExitInstance();
}
```

请注意，调用了基类的 `ExitInstance()` 函数，以允许对此事件进行默认处理。

现在使用 App Studio 创建对话框资源。此对话框用于显示应用程序类中定义的 WSADATA 结构所包含的信息。将对话框的标题设为“WinSock 信息”，ID 设为 IDD_DIALOG_WINSOCK_INFO。默认情况下，App Studio 会在对话框中包含“确定”和“取消”按钮；请移除“取消”按钮，因为此对话框仅用于提供信息，其返回值会被直接忽略。要显示存储在 WSADATA 结构中的数据，我们需要几个字段。此示例使用 EDIT 控件来显示这些信息。每个 EDIT 控件前面都有一个 STATIC 文本控件，用作标签。创建五个垂直对齐的 EDIT 控件，名称如下：IDC_EDIT_VERSION、IDC_EDIT_DESCRIPTION、IDC_EDIT_STATUS、IDC_EDIT_MAXIMUM_SOCKETS 和 IDC_EDIT_MAXIMUM_DATAGRAM_SIZE。

在 App Studio 中，选中“WinSock 信息”对话框，运行 ClassWizard 创建与此对话框资源关联的类。将类命名为 CWinSockInfoDlg，基类为 CDialog。将 ClassWizard 为此类创建的源文件名称更改为 INFODLG.CPP 和 INFODLG.H。

创建类后，使用 ClassWizard 创建一个函数来处理对话框初始化阶段。选中 CWinSockInfoDlg 类名后，在 ClassWizard 的 Object IDs 列表中选择 CWinSockInfoDlg。执行此操作后，ClassWizard 窗口的 Messages 部分会填满大量内容。这些是可能发送给 CWinSockInfoDlg 类的 Windows 消息。向下滚动到 WM_INITDIALOG 消息，然后单击 Add Function 按钮。ClassWizard 会自动生成一个名为 OnInitDialog() 的存根函数。

退出 App Studio 并编辑 INFODLG.CPP 文件。添加代码，使用存储在 WSADATA 结构中的信息填充对话框的字段。WSADATA 结构是 CWSinfoApp 类的公共成员变量，因此您可以通过获取指向应用程序对象的指针，从 CWinSockInfoDlg 类访问它。AfxGetApp() 函数用于此目的。完成后，OnInitDialog() 函数应如下所示：

```cpp
BOOL CWinSockInfoDlg::OnInitDialog()
{
    CDialog::OnInitDialog();

    // initialize the fields of the dialog box

    CWSinfoApp *pApp = (CWSinfoApp *)AfxGetApp();  // pointer to app
    LPWSADATA pWsaData = &(pApp->m_wsaData);       // pointer to app's WinSock info
    char pszMsg[100];                              // buffer to use for formatting

    wsprintf(pszMsg, "%d.%d",
        (int)(HIBYTE(pWsaData->wVersion)), (int)(LOBYTE(pWsaData->wVersion)));
    SetDlgItemText(IDC_EDIT_VERSION, pszMsg);
    SetDlgItemText(IDC_EDIT_DESCRIPTION, pWsaData->szDescription);
    SetDlgItemText(IDC_EDIT_STATUS, pWsaData->szSystemStatus);
    wsprintf(pszMsg, "%d", pWsaData->iMaxSockets);
    SetDlgItemText(IDC_EDIT_MAXIMUM_SOCKETS, pszMsg);
    wsprintf(pszMsg, "%u", pWsaData->iMaxUdpDg);
    SetDlgItemText(IDC_EDIT_MAXIMUM_DATAGRAM_SIZE, pszMsg);

    return TRUE;  // return TRUE unless you set the focus to a control
}
```

现在您已有足够的代码来启动 WinSock 并填充信息对话框。唯一缺少的是启动该对话框的方法。启动 App Studio 并编辑菜单资源。在 Help 选择项下添加一个菜单项，标题为“WinSock 信息”，ID 为 ID_WINSOCK_INFO。运行 ClassWizard 为 ID_WINSOCK_INFO 消息生成函数。为类名选择 CWSinfoApp，然后滚动浏览对象 ID，直到找到 ID_WINSOCK_INFO。在消息部分，选择 COMMAND，然后单击 Add Function 按钮。使用 OnWinsockInfo 作为函数名来处理此菜单项被选中的事件。OnWinsockInfo 成员函数的代码如下所示：

```cpp
void CWSinfoApp::OnWinsockInfo()
{
    // If WinSock startup was successful, display an informational
    // dialog box; otherwise, display an error message

    if (m_bWinSockOK)
    {
        CWinSockInfoDlg dlg;
        dlg.DoModal();
    }
    else
    {
        char pszError[100];
        if (m_nWinSockError)
            wsprintf(pszError, "WinSock startup failed with error %d",
                m_nWinSockError);
        else
```
