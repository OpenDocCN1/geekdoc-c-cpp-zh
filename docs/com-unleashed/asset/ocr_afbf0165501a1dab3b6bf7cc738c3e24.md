**Table 21.1** Results of the Two Loops

| Class | Milliseconds | Percent Performance Increase |
|---|---:|---:|
| CVersionOne | 2975 | n/a |
| CVersionTwo | 2063 | 30.65 |

The ATL and Visual Basic projects can be found in the Chapter21 directory on the CD-ROM.

> **Note**
> 
> If you compile the Algorithm COM object in anything but debug mode, the efficient compiler that comes with Visual C++ sees that nothing is actually being done. The code reduces to nothing as the compiler optimizes the Perform() method to practically nothing. The Visual Basic program then simply gets a value of zero milliseconds for the time it takes to call each method.

# Avoid Registry Access

For standalone applications, Registry access is fast enough. That's because most stand-alone applications make a minimum number of trips to the Registry. A component that's part of a middle tier is an entirely different matter. Although the trip to the Registry exacts a small price in itself, it quickly compounds with a large-scale application.

I wrote a COM object that opens and reads a single Registry string 10,000 times to find out a hard number for how expensive Registry access really is. The code fragment that does the work is shown in Listing 21.1.

# Listing 21.1  Reading a Registry String 10,000 Times

```
void CWorker::ReadRegistryString( HKEY hKey, DWORD dwSize,
    const char *pszKeyname, const char *pszDataname, void *pRetbuffer )
{
    HKEY hKey;

    if( RegOpenKeyEx( hKey, pszKeyname, 0, KEY_ALL_ACCESS, &hKey )
        != ERROR_SUCCESS )
        return;

    RegQueryValueEx( hKey, pszDataname, NULL, NULL,
        (unsigned char *) pRetbuffer, &dwSize );
}
```