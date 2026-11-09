
另一台服务器，它正代表客户端调用该服务器。模拟级别表示客户端已授予服务器多少权限。

不使用伪装的模拟可行，但可能不是最佳选择，因为在某些情况下，最终服务器需要知道初始调用者的身份。如果不使用伪装，就无法实现这一点。伪装会呈现初始调用者的身份；没有伪装，就很难确保只有经过授权的客户端才能访问远程计算机。当使用模拟但不使用伪装时，向下游服务器呈现的身份是直接调用进程的身份。

没有模拟，伪装也没有用。只有当客户端将模拟级别设置为“模拟”或“委派”时，伪装才有意义。（在较低的模拟级别下，服务器无法进行伪装调用。）伪装是否成功取决于模拟级别（它表示服务器代表客户端行事所拥有的权限大小）以及跨过的计算机边界数量。下面的讨论解释了伪装和模拟级别的选择如何影响模拟期间发生的情况。

在某些情况下，当客户端将模拟级别设置为 RPC_C_IMP_LEVEL_IMPERSONATE 时，服务器设置伪装是合理的。但是，存在某些限制。如果原始客户端将模拟级别设置为 RPC_C_IMP_LEVEL_IMPERSONATE，则中间服务器（在同一台计算机上作为客户端行事）只能跨一个计算机边界进行伪装。这是因为模拟级模拟令牌只能跨一个计算机边界传递。跨过计算机边界后，只能访问本地资源。向服务器呈现的身份取决于所设置的伪装类型。如果未设置伪装，则向服务器呈现的身份将是进行直接调用的进程的身份。

要跨多个计算机边界进行伪装，必须同时指定适当的伪装能力标志和委派级模拟。使用这种类型的模拟时，客户端的本地凭据和网络凭据都会提供给服务器，因此模拟令牌可以跨任意数量的计算机边界。同样，向服务器呈现的身份取决于所设置的伪装类型。如果在委派级模拟中未设置伪装，则向服务器呈现的身份是进行调用的进程的身份。

例如，假设进程 A 调用 B，B 调用 C。B 已设置伪装，A 已将模拟级别设置为“模拟”。如果 A、B 和 C 在同一台计算机上，则从 A 向 B 再向 C 传递模拟令牌将可行。但如果 A 和 C 在同一台计算机上，而 B 不在，则令牌在 A 与 B 之间传递可行，但从 B 到 C 不可行。从 B 到 C 的调用将失败，因为 B 在伪装时无法调用 C。但是，如果 A 将模拟级别设置为“委派”，则令牌可以从 B 传递到 C，因此该调用可以成功。

## CoImpersonateClient() 和 CoRevertToSelf()

CoImpersonateClient() 允许 COM 服务器采用调用客户端进程的身份。当 COM 服务器没有足够的访问权限来代表调用客户端进程执行任务时，您会希望这样做。当 COM 服务器希望停止模拟客户端并恢复自身身份时，应调用 CoRevertToSelf()。

清单 12.8 显示了这两个辅助函数的实现。

**清单 12.8** CoImpersonateClient() 和 CoRevertToSelf() 的实现

```cpp
WINOLEAPI CoImpersonateClient()
{
    IServerSecurity *pss;
    ::CoGetCallContext(IID_IServerSecurity, (void **)&pss);
    HRESULT hresult = pss->ImpersonateClient();
    pss->Release();
    return hresult;
}
WINOLEAPI CoRevertToSelf()
{
    IServerSecurity *pss;
    ::CoGetCallContext(IID_IServerSecurity, (void**)&pss);
    HRESULT hresult = pss->RevertToSelf();
    pss->Release();
    return hresult;
}
```

CoImpersonateClient() 和 CoRevertToSelf() 函数使用在服务器中实现的 IServerSecurity 接口。清单 12.9 是该接口的 MIDL 定义。需要注意的是，对于标准封送处理，IServerSecurity 几乎总是在存根级别完成。唯一的例外是响应自定义封送处理时。

正如其名称所示，IServerSecurity 的 CoGetCallContext() 方法仅对当前调用有效。

**清单 12.9** IServerSecurity 接口的 MIDL 定义

```cpp
interface IServerSecurity : IUnknown
{
    HRESULT QueryBlanket(
        [out] DWORD    *pAuthnSvc,
        [out] DWORD    *pAuthzSvc,
        [out] OLECHAR **pServerPrinName,
        [out] DWORD    *pAuthLevel,
        [out] DWORD    *pImplevel,
        [out] void     **pPrivs,
        [out] DWORD    *pCapabilities
    );

    HRESULT ImpersonateClient();

    HRESULT RevertToSelf();

    BOOL IsImpersonating();
};
```

还有另一个函数可用于告知服务器当前是否正在模拟客户端。此函数是 IServerSecurity::IsImpersonating()。此方法没有辅助函数，但您可以实现自己的辅助函数，如清单 12.10 所示。从代码中您可能会注意到，我们位于服务器中。这意味着此前已调用 ImpersonateClient()。

**清单 12.10** CoIsImpersonating() 的实现

```cpp
BOOL CoIsImpersonating()
{
    IServerSecurity *pss;
    CoGetCallContext(IID_IServerSecurity, (void**)&pss);
    BOOL b = pss->IsImpersonating();
    pss->Release();
    return b;
}
```

IServerSecurity 接口的最后一个函数是 IServerSecurity::QueryBlanket() 方法。此方法有一个名为 CoQueryClientSecurity() 的辅助函数，其实现如清单 12.11 所示。

**清单 12.11** CoQueryClientSecurity() 的实现

```cpp
WINOLEAPI CoQueryClientSecurity()
{
    IServerSecurity *pss;
    ::CoGetCallContext(IID_IServerSecurity, (void**)&pss);
    HRESULT hresult = pss->QueryBlanket();
    pss->Release();
    return hresult;
}
```

此函数查询调用服务器的客户端的安全设置。

## 伪装

前面描述的委派模拟级别通常称为伪装。这种类型的模拟在对其他服务器进行调用期间，通过用客户端的身份来伪装中间服务器的身份，从而隐藏服务器的真实身份。

## 声明式安全

如您在第 8 章所学，可以在注册表中声明 COM 服务器的安全设置。这有时称为声明式安全或每进程安全。请注意，声明式安全和每进程安全并不完全相同。声明式安全由 Windows 系统注册表中的设置组成，这些设置在启动或访问 COM 服务器时使用。每进程安全包括注册表设置，但也包括用于操纵整个进程的 COM 服务器设置的其他机制，例如函数 `CoInitializeSecurity()`。

在第 13 章“配置和错误处理”中，您将学习如何使用名为 `DCOMCNFG` 和 `OLEView` 的两个工具为 COM 服务器配置每进程安全设置。

## 编程式安全

在本章前面，您学习了编程式安全的两个要素——用于模拟客户端的 `IServerSecurity` 接口，以及用于设置每进程安全的 `CoInitializeSecurity()` 函数。`CoInitializeSecurity()` 函数会为您的进程创建安全毯；也就是说，创建安全设置。

### 安全毯

那么什么是安全毯？安全毯是一组安全属性。这些安全属性包括以下内容：

- 身份验证服务
- 授权服务
- 主体名称
- 身份验证级别
- 模拟级别
- 身份验证标识
- 能力
- ACL
