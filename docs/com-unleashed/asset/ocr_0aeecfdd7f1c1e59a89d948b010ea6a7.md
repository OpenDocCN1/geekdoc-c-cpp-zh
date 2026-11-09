enables you to have multiple versions of your COM class installed on the same machine. Each version will be tagged with an incrementing integer suffix.

# Version-Independent ProgIDs

It is convenient to also have a version-independent ProgID. The version-independent ProgID has the following syntax:

```
MyModuleName.MyObjectName
```

This ProgID makes it possible for client programmers to use objects without having to check which version of the object is installed on the system.

# AppIDs

AppIDs are subkeys of the key HKEY_CLASSES_ROOT\AppID.

The AppID key (see Figure 8.6) has the following structure:

```
HKEY_CLASSES_ROOT
{
  appid-as-guid
    RemoteServerName = { DNS or UNC of server } // client machine only
    DLLSurrogate = { path\surrogate.exe or NULL } // DLLhost.exe
      // server machine only
    LaunchPermission = REG_BINARY { self-relative security descriptor }
    AccessPermission = REG_BINARY { self-relative security descriptor }
    ActivateAtStorage = { Y or N }
    LocalService =
      ServiceParameters =
      RunAs = { none | "Interactive User" | user account }
        AuthenticationLevel =
```

**FIGURE 8.6**  
*The AppID key structure.*

![](bbox=[0.249, 0.661, 0.667, 0.807])

The AppID provides information on how to launch the COM server. COM servers can be configured to run remotely, with security, permissions, and as services.