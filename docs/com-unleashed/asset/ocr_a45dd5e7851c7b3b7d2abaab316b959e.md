# **FIGURE 8.8**  
*The CLSID key structure.*

![](bbox=[0.247, 0.12, 0.666, 0.267])

Listing 8.5 can be used to configure the CLSID system registry key.

# **LISTING 8.5**  Configuring the CLSID Registry Key

```
```cpp
int BuildCLSIDKey(CLSID clsid, LPSTR szDescription,
                  LPSTR szProgID, LPSTR szProgIDVersionIndependent)
{
    // build the CLSID
    LPOLESTR oleStr = NULL;
    LPSTR str = NULL;
    ::StringFromCLSID(clsid, &oleStr);
    int i = ::WideCharToMultiByte(CP_ACP, 0, oleStr, -1, str,
                                   0, NULL, NULL);
    str = new char[i+1];
    ::WideCharToMultiByte(CP_ACP, 0, oleStr, -1, str,
                          i, NULL, NULL);

    // build the subkey
    LPSTR str2 = NULL;
    LPSTR strCLSID = "CLSID";
    str2 = new char[::lstrlen(strCLSID)+::lstrlen(str)+2];
    ::lstrcpy(str2, strCLSID);
    ::lstrcat(str2, "\\");
    ::lstrcat(str2, str);

    // set description
    CRegistry key(HKEY_CLASSES_ROOT, str2);
    key.SetValue(NULL, szDescription);
    delete[] str2;

    // build CLSID\\{CLSID}\\ProgID string
    LPSTR strProgID = "ProgID";
    str2 = new char[::lstrlen(strCLSID)+::lstrlen(str)
                    +::lstrlen(strProgID)+3];
    ::lstrcpy(str2, strCLSID);
    ::lstrcat(str2, "\\");
    ::lstrcat(str2, str);
    ::lstrcat(str2, "\\");
    ::lstrcat(str2, strProgID);
```
```