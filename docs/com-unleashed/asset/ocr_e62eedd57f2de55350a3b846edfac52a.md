**TABLE 18.2 Continued**

| Method | What It Does |
|---|---|
| `GetOriginalCreatorSID()` | Retrieves the security ID of the base process that initiated the activity in which the current object is executing |
| `ReleaseSID()` | Releases the security ID returned by one of the other `ISecurityProperty` methods |

Listing 18.1 shows a new internal Sum class method that discovers the direct caller's SID.

# **LISTING 18.1** Discovering the Direct Caller's SID

```
void CSum::GetDirectCallerSID( BSTR * pbstrSid )
{
    //Initialize the security interface pointer,
    // the binary SID and the string SID
    ISecurityProperty * pSecurityProperty = NULL;
    PSID pSID = NULL;
    * pbstrSid = NULL;

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