
## PART III

**Table 18.1 Authentication Levels**

| Level | Description |
|---|---|
| None | No security checking occurs on communication to or from this application. |
| Connect | Security checking occurs only upon the initial connection. |
| Call | Security checking occurs on every call. |
| Packet | The sender's identity is encrypted. |
| Packet Integrity | The sender's identity and signature are encrypted (guaranteeing integrity). |
| Packet Privacy | The entire packet is encrypted (guaranteeing privacy). |

### Procedural COM+ Security

You've seen how an administrator can completely secure an application down to the interface level. I've also introduced some of the concerns, especially the importance of administrator competency. It is no small task to configure a free-form component program, consisting of applications and components that change machines and processes over time.

In order to reduce the declarative burden on administrators or simply to get more granular control of the security mechanism, developers might want to code in their own security features. In this section, you'll combine some declarative features with some low-level security operations in code.

The example used throughout is a security-aware version of your Stateful Sum class. In order to follow along with the examples, you need to create a new application called SecureSum. Add the Stateful component to the application and add two roles, Admins and Accumulators. Add one user account to Admins and another to Accumulators, so that you can test both roles.

### Identifying Users

Your security endeavors here are limited to the Accumulate() method in your Sum class. One of the first tasks that I'd like you to perform is that of ensuring that each user has his own private copy of the accumulated total. In a multiuser enterprise, this is easier said than done. Your object supports deactivation, so you probably still need to use the Shared Property Manager to maintain state information between calls. However, you need to name the property in such a way as to make it unique among all users.

Of course, IAccessControl object should not be changed. If EOAC_ACCESS_CONTROL is specified, the dwAuthnLevel cannot be NULL.

The CoInitializeSecurity() function returns an error if both the EOAC_APPID and EOAC_ACCESS_CONTROL flags are set.

If neither the EOAC_APPID nor the EOAC_ACCESS_CONTROL flag is specified in dwCapabilities, pVoid must be a pointer to a Win32 SECURITY_DESCRIPTOR. A security descriptor contains two ACLs: the discretionary ACL (DACL), which indicates who is (and who is not) allowed to call the process, and the system ACL (SACL), which contains audit information. COM+ looks for the COM_RIGHTS_EXECUTE flag in the DACL to find out which callers are permitted to connect to the process's objects. The SACL must be NULL. A DACL with no ACEs allows no access. A NULL DACL allows calls from anyone.

If pVoid is a security descriptor, the owner and group of the SECURITY_DESCRIPTOR must be set—applications should call AccessCheck (not IsValidSecurityDescriptor) to ensure that their security descriptor is correctly formed prior to calling CoInitializeSecurity(). COM+ copies the specified security descriptor. If the application passes a NULL security descriptor, COM+ constructs one that allows calls from anyone.

When a CAPI handle is specified for the SSL entry in pAuthList, the CAPI handle must not be freed until CoUninitialize() is called. If the list is specified but there is no entry for SSL, COM+ tries to find a default identity the first time COM+ negotiates SSL as the authentication service. If that succeeds, COM+ saves that identity as the default. Otherwise, the client is anonymous for SSL.

### ISecurityProperty Interface

COM+ provides the ISecurityProperty interface as a means to discover various caller process SIDs. ISecurityProperty is obtained through a QueryInterface() call on an object's IUnknown pointer. Each ISecurityProperty method call returns the respective SID pointer. Because you are getting back a system-allocated resource, you must release the resource when you are finished with it by calling ReleaseSID(). Table 18.2 shows the methods.

**Table 18.2 ISecurityProperty Methods**

| Method | What It Does |
|---|---|
| `GetDirectCallerSID()` | Retrieves the security ID of the external process that called the currently executing method |
| `GetDirectCreatorSID()` | Retrieves the security ID of the external process that directly created the current object |
| `GetOriginalCallerSID()` | Retrieves the security ID of the base process that initiated the call sequence from which the current method was called |
| `GetOriginalCreatorSID()` | Retrieves the security ID of the base process that initiated the activity in which the current object is executing |
| `ReleaseSID()` | Releases the security ID returned by one of the other `ISecurityProperty` methods |

Listing 18.1 shows a new internal Sum class method that discovers the direct caller's SID.

**LISTING 18.1 Discovering the Direct Caller's SID**

```cpp
void CSum::GetDirectCallerSID( BSTR * pbstrSid )
{
    //Initialize the security interface pointer,
    // the binary SID and the string SID
    ISecurityProperty * pSecurityProperty = NULL;
    PSID pSID = NULL;
    *pbstrSid = NULL;

    //Get the security property interface
    // from the ObjectContext
    m_spObjectContext->QueryInterface( IID_ISecurityProperty,
                                       (void**)&pSecurityProperty );

    if ( NULL == pSecurityProperty )
        return;

    //Get the direct caller's binary SID
    HRESULT hr = pSecurityProperty->GetDirectCallerSID( &pSID );
    if ( FAILED(hr) )
        return;

    //Convert the binary SID to a text string and release
    // the binary SID and security property interface
    SidToString( pSID, pbstrSid );
    pSecurityProperty->Release();
}
```

As you can see, the steps are quite simple. You get the security property interface and make the GetDirectCallerSID() call. The catch here is that COM+ gives you a binary SID. If you want to use this SID to create an SPM property, you'll have to convert it to text (all SPM properties have text names). The helper function SidToString() does the dirty work. Unfortunately, this is not a system call. Listing 18.2 shows the code.

**LISTING 18.2 Converting a Binary SID to Text**

```cpp
bool CSid::SidToString(     PSID pSid,                 //Binary Sid
                            BSTR * pbsSid )             //String Sid
{
    //Test Sid for validity
    if(!IsValidSid(pSid))
        return false;

    //Test BSTR for validity
    if(NULL == pbsSid)
        return false;

    //Set up working buffer and initialize input BSTR
    WCHAR wsSid[128];
    *pbsSid = NULL;

    //Obtain SidIdentifierAuthority
    PSID_IDENTIFIER_AUTHORITY psia = GetSidIdentifierAuthority(pSid);

    //Prepare S-SID-REVISION
    DWORD dwSidLength = swprintf( wsSid, L"S-%lu-", SID_REVISION );

    //Prepare SidIdentifierAuthority
    if ( ( psia->Value[0] != 0 ) || ( psia->Value[1] != 0 ) )
    {
        dwSidLength += swprintf(wsSid + dwSidLength,
                                L"%02hx%02hx%02hx%02hx%02hx%02hx",
                                (USHORT)psia->Value[0],
                                (USHORT)psia->Value[1],
                                (USHORT)psia->Value[2],
                                (USHORT)psia->Value[3],
                                (USHORT)psia->Value[4],
                                (USHORT)psia->Value[5]);
    }
    else
    {
        dwSidLength += swprintf(wsSid + dwSidLength,
                                L"%lu",
                                (ULONG)(psia->Value[5]      ) +
                                (ULONG)(psia->Value[4] <<  8) +
                                (ULONG)(psia->Value[3] << 16) +
                                (ULONG)(psia->Value[2] << 24) );
    }

    //Loop through SidSubAuthorities
    DWORD dwSubAuthorities = *GetSidSubAuthorityCount(pSid);
    for (DWORD dwCounter=0; dwCounter<dwSubAuthorities; dwCounter++)
    {
        dwSidLength += swprintf(wsSid + dwSidLength,
                                L"-%lu",
```
