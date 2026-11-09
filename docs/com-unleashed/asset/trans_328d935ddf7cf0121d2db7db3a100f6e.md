
最后三个设置等效于 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Ole` 注册表项中的 `LegacyAuthenticationLevel`、`LegacyImpersonationLevel` 和 `LegacySecureReferences` 设置。这些内容已在第 8 章讨论过。这些设置被称为旧版设置，因为较新的 COM+ 对象应调用 `CoInitializeSecurity()` 来设置这些设置。在 DCOM+ 之前创建的旧版 COM+ 对象没有调用此函数，因为当时该函数尚不可用。COM+ 在代表这些旧版对象调用 `CoInitializeSecurity()` 时会使用这些旧版设置。

## 默认安全

DCOMCNFG 属性表对话框的第三个选项卡是“默认安全”属性页，如图 13.3 所示。此选项卡显示三个类别：默认访问权限、默认启动权限和默认配置权限。它们共同构成 COM+ 对象的默认安全设置。

**图 13.3**  
*DCOMCNFG*  
*默认安全*  
*页。*

![](img/112c2326f49d26b8d59aa054e14c5747_357_0.png)

### 设置访问权限

在“默认访问权限”框中单击“编辑默认值”时，可以修改 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Ole` 注册表项中的 `DefaultAccessPermission` 值。此设置确定谁可以调用未指定自定义访问权限的对象。

让我们从理论转向实践。在本章前面“创建自动化服务器”一节中，你创建并安装了一个可用作示例的 COM+ 服务器。清单 13.6 展示了使用 DCOMCNFG 更改配置如何反映在对 COM+ API 的成功和失败调用中。

**清单 13.6 创建并访问测试对象**

```cpp
#include <windows.h>

HRESULT LaunchAndAccess()
{
    // HRESULT returned from last automation call
    HRESULT hresult;
    // IDISPATCH interface pointer for the existing object
    LPDISPATCH pdisp = NULL;
    // hold exception info here
    EXCEPINFO excepinfo;
    // hold argument error here
    UINT uArgErr;

    // Convert the progid to a clsid
    CLSID clsid;
    hresult = ::CLSIDFromProgID(OLESTR("MyObject.MyObject.1"),
                                &clsid);
    if (hresult)
    {
        // CLSIDFromProgID failed
        return hresult;
    };

    // Create the instance of the object
    LPUNKNOWN punk;
    hresult = ::CoCreateInstance(clsid, NULL, CLSCTX_SERVER,
                                 IID_IUnknown, (LPVOID FAR *)&punk);

    if (hresult)
    {
        // CoCreateInstance failed
        return hresult;
    };

    // Retrieve the interface pointer
    hresult = punk->QueryInterface(IID_IDispatch,
                                   (LPVOID FAR *)&pdisp);

    if (hresult)
    {
        // QueryInterface failed
        return hresult;
    };

    // Release the IUnknown reference.
    hresult = punk->Release();

    // return an exception if the dispatch pointer is NULL
    if (pdisp==NULL)
    {
        return E_UNEXPECTED;
    }

    // Retrieve the dispatch id for the function name
    DISPID dispid;
    BSTR bstr = ::SysAllocString(OLESTR("MyProperty"));
    hresult = pdisp->GetIDsOfNames(IID_NULL, &bstr, 1,
                                  LOCALE_USER_DEFAULT,
                                  &dispid);
    ::SysFreeString(bstr);
    if (hresult)
    {
        // GetIDsOfNames failed
        return hresult;
    };

    // Invoke the property GET
    DISPPARAMS dispparams = {0};
    VARIANTARG variantarg;
    VariantInit(&variantarg);
    memset(&excepinfo, 0, sizeof(EXCEPINFO));
    uArgErr = 0;
    hresult = pdisp->Invoke(dispid, IID_NULL,
                           LOCALE_USER_DEFAULT,
                           DISPATCH_PROPERTYGET,
                           &dispparams, &variantarg,
                           &excepinfo, &uArgErr);
    if (hresult)
    {
        // Invoke failed
        return hresult;
    };

    pdisp->Release();

    if (variantarg.lVal != 10)
    {
        // Wrong result
        return E_UNEXPECTED;
    };

    return S_OK;
}

int main(int, char **)
{
    CoInitialize(NULL);
    LaunchAndAccess();
    CoUninitialize();
    return 0;
}
```

我绝不建议更改这些设置。你最不希望发生的就是阻止某人修改此注册表项，因为应用程序必须有权访问此注册表项才能自行安装。因此，除非你有特定需求，例如远程安装应用程序或禁止用户安装 COM+ 对象，否则不建议修改此注册表项的安全权限。

## 配置 COM+ 服务器

单击“应用程序”选项卡可返回所有 COM+ 服务器的列表。如果从该列表中选择一个 COM+ 服务器并单击“属性”按钮，将出现一个单独属性表对话框，使你能够配置该 COM+ 服务器（见图 13.4）。

![](img/112c2326f49d26b8d59aa054e14c5747_361_0.png)

常规页上显示四个属性：应用程序名称、应用程序类型、应用程序级别和服务名称。DCOMCNFG 不允许你更改这些设置。这些设置也可在注册表中找到。应用程序名称是 `HKEY_CLASSES_ROOT\AppID\{my-clsid}` 注册表子项的键值。

应用程序类型是以下之一：

- 进程内处理程序
- 进程内服务器
- 本地服务
- 本地服务器
- 远程服务器

DCOMCNFG 会搜索对象的 `HKEY_CLASSES_ROOT\CLSID\{my-clsid}` 和 `HKEY_CLASSES_ROOT\AppID\{my-clsid}` 注册表子项。按前面列出的顺序，它首先找到的设置将用作该对象的应用程序类型。对于进程内处理程序、进程内服务器和本地服务器，该设置位于 `HKEY_CLASSES_ROOT\CLSID\{my-clsid}` 注册表子项中。对于本地服务和远程服务器，该设置位于 `HKEY_CLASSES_ROOT\AppID\{my-clsid}` 注册表子项中。有关 AppID 注册表树的详细讨论，请返回第 8 章。

应用程序位置是上一段讨论的应用程序类型注册表子项在注册表中的值名称。对于本地服务器、进程内服务器和进程内处理程序，这是模块的本地路径。对于本地服务，这是服务的名称。对于远程服务器，这是远程服务器的名称。

### 服务器位置

DCOMCNFG 中的“位置”选项卡有三个复选框，如图 13.5 所示。

![](img/112c2326f49d26b8d59aa054e14c5747_362_0.png)

第一个复选框启用或禁用“在存储处激活”。这等效于 ActivateAtStorage 注册表设置。“在存储处激活”意味着 COM+ 对象在数据文件所在的计算机上启动。

第二个复选框指示 COM+ 启动并连接到本地计算机上的 COM+ 服务器。第三个复选框指示 COM+ 启动并连接到远程计算机上的 COM+ 服务器。选中此按钮会将 RemoteServer 注册表设置写入 `HKEY_CLASSES_ROOT\AppID\{my-clsid}` 子项，并启用编辑框和浏览按钮控件。这些控件使你能够使用资源管理器风格的浏览器指定远程服务器名称。

运行清单 13.6 时，`CoCreateInstance()` 调用会失败，因为你的用户账户无法启动服务器。

### 设置启动权限

此页上的第二组控件是启动权限单选按钮和编辑控件。它们修改 `HKEY_CLASSES_ROOT\AppID\{my-clsid}` 子项中的 LaunchPermission 注册表设置。

选择“使用自定义启动权限”并单击“编辑”。“注册表值权限”对话框将出现。将设置更改为“拒绝你的用户账户的启动权限”。运行清单 13.6 时，`CoCreateInstance()` 调用会失败，因为你的用户账户没有启动权限。

如果手动启动服务器并运行清单 13.6，`CoCreateInstance()` 会成功。和之前一样，对 `CoCreateInstance()` 的调用不需要启动服务器，因为它已经在运行。

### 设置配置权限

此页上的最后一组控件是配置权限单选按钮和“编辑”控件。它们修改 `HKEY_CLASSES_ROOT\AppID\{my-clsid}` 子项的注册表安全权限。此设置确定谁可以修改对象的配置。

选择“使用自定义配置权限”并单击“编辑”。“注册表项权限”对话框出现。如果你尚未更改 COM+ 的默认配置权限，则接下来出现的对话框应与图 13.7 所示类似。

*图 13.7*  
*注册表项权限。*

![](img/112c2326f49d26b8d59aa054e14c5747_364_0.png)

在尝试后续步骤之前，请确保你拥有管理员密码。你可以通过移除 Everyone 项来演示自定义配置权限更改的效果。以非管理员用户身份登录计算机。

打开 REGEDIT 和 REGEDT32，尝试查看该 COM+ 服务器的 `HKEY_CLASSES_ROOT\AppID\{my-clsid}` 注册表子项。你应该会看到与图 13.8 和图 13.9 所示类似的屏幕。
