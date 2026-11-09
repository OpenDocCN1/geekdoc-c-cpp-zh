# LISTING 13.16  IDL for IErrorInfo

```
```idl
interface IErrorInfo: IUnknown
{
    HRESULT GetGUID([out] GUID * pGUID);
    HRESULT GetSource([out] BSTR * pBstrSource);
    HRESULT GetDescription([out] BSTR * pBstrDescription);
    HRESULT GetHelpFile([out] BSTR * pBstrHelpFile);
    HRESULT GetHelpContext([out] DWORD * pdwHelpContext);
}
```
```

I used the IErrorInfo::GetDescription() and IErrorInfo::GetSource() methods to retrieve only the most basic information. All the source code for the IErrorInfo sections is included on the CD-ROM as errorinfo. It can be found in the errorinfo subdirectory in the chapter13 directory. If you step through the code of the two clients provided, you have a better feel for the power of these three error handling interfaces.

# Summary

This chapter gives you a solid basis for understanding how to configure DCOM and to handle errors. You first learned how to use the DCOMCNFG utility so the COM+ works correctly on client machines. The sections in the registry that pertain to COM+ configuration were discussed, and you learned what to look out for when examining the registry. Several examples using Visual C++ were shown—these will help you write special utilities to automate some configuration operations.

Client COM+ errors were discussed along with ways to fix the client configuration so that the errors are fixed. This is an important section because the client configuration must be correct or all your COM+ development will have been in vain.