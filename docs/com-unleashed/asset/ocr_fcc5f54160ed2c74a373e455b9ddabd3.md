Both the client and server create their security blankets by calling the `CoInitializeSecurity()` function. If either the client or server fails to call this function, COM calls the function with default values on behalf of the process.

COM uses the client's and server's security blankets to negotiate the proxy's security blanket. COM selects an authentication service (and an authorization service and principal name that work with the service) that is available on both the client and server. COM selects the highest authentication level specified by the client or server. COM selects the client's impersonation level, authentication identity (that works with the selected authentication server), and capabilities.

The security blanket is negotiated when the proxy is created. After the proxy is created, the client has control over the proxy using the `IClientSecurity` interface described in the next section.

# IClientSecurity

Another interface called IClientSecurity allows the client to query and modify the security settings of the interface proxies. Listing 12.12 is the MIDL definition of the IClientSecurity interface.

# **LISTING 12.12** MIDL Definition of the IClientSecurity Interface

```
interface IClientSecurity : IUnknown
{
    HRESULT QueryBlanket
    (
        [in]  IUnknown             *pProxy,
        [out] DWORD                *pAuthnSvc,
        [out] DWORD                *pAuthzSvc,
        [out] OLECHAR              *pServerPrincName,
        [out] DWORD                *pAuthnLevel,
        [out] DWORD                *pImpLevel,
        [out] void                 **pAuthInfo,
        [out] DWORD                *pCapabilities
    );

    HRESULT SetBlanket
    (
        [in]  IUnknown             *pProxy,
        [in]  DWORD                 AuthnSvc,
        [in]  DWORD                 AuthzSvc,
        [in]  OLECHAR              *pServerPrincName,
        [in]  DWORD                 AuthnLevel,
        [in]  DWORD                 ImpLevel,
        [in]  void                 *pAuthInfo,
```