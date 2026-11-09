function. This is done automatically in a module named `module.dll` by executing the command line `REGSVR32 module.dll`. To unregister, remove the system registry entries by running the `DLLUnregisterServer` function. This is done automatically in a module named `module.dll` by executing the command line `REGSVR32 /U module.dll`.

Self-registering DLLs should include the string `OLESelfRegister` in its VERSIONINFO resource. Listing 8.7 shows where the OLESelfRegister string occurs in the VERSIONINFO resource.

# **LISTING 8.7** OLESelfRegister String in VERSIONINFO Resource

```
VS_VERSION_INFO VERSIONINFO
BEGIN
    BLOCK "StringFileInfo"
    BEGIN
        BLOCK "040904E4" // Lang=US English, CharSet=Windows Multilingual
        BEGIN
            ...
            VALUE "OLESelfRegister", "\0"
        END
    END
END
...
END
...
```

Your DLLRegisterServer and DLLUnregisterServer functions must be exported from your DLL, and they must not contain C++ name mangling. If the exported functions have C++ name mangling, clients such as REGSVR32 will fail when calling the functions. The stubs for implementing DLLRegisterServer and DLLUnregisterServer are shown in Listing 8.8.

# **LISTING 8.8** Stubs for Implementing DLLRegisterServer

```
//...
// DllRegisterServer
//...
STDAPI DllRegisterServer()
{
    // use RegCreateKey() and RegSetValue() to add keys
    ...
    return NOERROR;
}

//...
// DllUnregisterServer
//...
```