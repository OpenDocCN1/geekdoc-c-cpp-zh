# CoImpersonateClient() and CoRevertToSelf()

CoImpersonateClient() allows the COM server to take on the identity of the calling client process. You'll want to do this when the COM server does not have sufficient access rights to perform a task on behalf of the calling client process. CoRevertToSelf() should be called when the COM server wants to discontinue impersonating the client and revert back to its own identity.

Listing 12.8 shows the implementation of these two helper functions.

# **LISTING 12.8**  Implementation of CoImpersonateClient() and CoRevertToSelf()

```
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

# **LISTING 12.9**  MIDL Definition of the IServerSecurity Interface

```
interface IServerSecurity : IUnknown
{
    HRESULT QueryBlanket
    {
        [out] DWORD    *pAuthnSvc,
        [out] DWORD    *pAuthzSvc,
```