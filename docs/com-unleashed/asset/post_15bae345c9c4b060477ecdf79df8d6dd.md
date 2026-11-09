
another server it is calling on behalf of the client. The impersonation level indicates how much authority the client has given the server.

Impersonation without cloaking works, but it might not be the best choice because, in some cases, the final server needs to know the identity of the initial caller. This cannot be achieved without using cloaking. Without cloaking, which presents the identity of the initial caller, it is difficult to ensure that only authorized clients can access a remote machine. When impersonation is used without cloaking, the identity presented to a downstream server is that of the immediate calling process.

Cloaking is not useful without impersonation either. Cloaking only makes sense when the client has set an impersonation level of impersonate or delegate. (With lower impersonation levels, the server cannot make cloaked calls.) Whether cloaking is successful depends on the impersonation level, which indicates how much authority the server has to act on behalf of the client and on the number of machine boundaries crossed. The following discussion explains how the choice of cloaking and impersonation level affect what happens during impersonation.

In some situations, it makes sense for the server to set cloaking when the client sets the impersonation level to RPC_C_IMP_LEVEL_IMPERSONATE. However, certain limitations are in effect. If the original client sets the impersonation level to RPC_C_IMP_LEVEL_IMPERSONATE, the intermediate server (acting as a client on the same machine) can cloak across only one machine boundary. This is because an impersonate-level impersonation token can only be passed across one machine boundary. After the machine boundary has been crossed, only local resources can be accessed. The identity presented to the server depends on the type of cloaking that is set. If no cloaking is set, the identity presented to the server will be that of the process making the immediate call.

To cloak over multiple machine boundaries, you must specify both an appropriate cloaking capability flag and delegate-level impersonation. With this type of impersonation, both the local and network credentials of the client are given to the server, so the impersonation token can cross any number of machine boundaries. Again, the identity presented to the server depends on the type of cloaking that is set. If no cloaking is set with delegate-level impersonation, the identity presented to a server is that of the process making the call.

For example, suppose Process A calls B, and B calls C. B has set cloaking, and A has set the impersonation level to impersonate. If A, B, and C are on the same machine, passing the impersonation token from A to B and then to C will work. But if A and C are on the same machine, and B is not, passing the token will work between A and B, but not from B to C. The call from B to C will fail because B cannot call C while cloaking. However, if A sets the impersonation level to delegate, the token can be passed from B to C, so the call can succeed.

## CoImpersonateClient() and CoRevertToSelf()

CoImpersonateClient() allows the COM server to take on the identity of the calling client process. You'll want to do this when the COM server does not have sufficient access rights to perform a task on behalf of the calling client process. CoRevertToSelf() should be called when the COM server wants to discontinue impersonating the client and revert back to its own identity.

Listing 12.8 shows the implementation of these two helper functions.

**LISTING 12.8** Implementation of CoImpersonateClient() and CoRevertToSelf()

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

The functions CoImpersonateClient() and CoRevertToSelf() use the IServerSecurity interface that is implemented in the server. Listing 12.9 is the MIDL definition of this interface. It is important to note the IServerSecurity is almost always done at the stub level for standard marshaling. The only exception would be in response to custom marshaling.

IServerSecurity's CoGetCallContext() method is valid only for the current call as its name implies.

**LISTING 12.9** MIDL Definition of the IServerSecurity Interface

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

Another function is available to tell you whether the server is currently impersonating the client. This function is IServerSecurity::IsImpersonating(). No helper function exists for this method, but you can implement your own helper function, as shown in Listing 12.10. As you might notice from the code, we are in the server. This means the ImpersonateClient() has been previously called.

**LISTING 12.10** Implementation of CoIsImpersonating()

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

The last function of the IServerSecurity interface is the IServerSecurity::QueryBlanket() method. This method has a helper function called CoQueryClientSecurity() that is implemented as shown in Listing 12.11.

**LISTING 12.11** Implementation of CoQueryClientSecurity()

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

This function queries the security settings of the client that invoked the server.

## Cloaking

The delegate impersonation level described previously is generally referred to as cloaking. This type of impersonation hides the server’s true identity during calls to other servers by disguising the intermediate server’s identity with the identity of the client.

## Declarative Security

As you learned in Chapter 8, it is possible to declare the security for a COM server in the registry. This is sometimes called declarative security or per-process security. Note that declarative security and per-process security are not entirely the same. Declarative security consists of the settings in the Windows system registry that are used when a COM server is launched or accessed. Per-process security includes the registry settings but also includes other mechanisms of manipulating the COM server’s settings for the entire process, such as the function `CoInitializeSecurity()`.

In Chapter 13, “Configuring and Error Handling,” you learn how you can use two tools called `DCOMCNFG` and `OLEView` to configure the per-process security settings for your COM servers.

## Programmatic Security

Earlier in this chapter, you learned two elements of programmatic security—the `IServerSecurity` interface that you used to impersonate the client and the `CoInitializeSecurity()` function used to set per-process security. The `CoInitializeSecurity()` function creates a security blanket for your process; that is, the security settings.

### Security Blankets

So what is a security blanket? A security blanket is a set of security properties. Those security properties include the following:

- Authentication service
- Authorization service
- Principal name
- Authentication level
- Impersonation level
- Authentication identity
- Capabilities
- ACL
