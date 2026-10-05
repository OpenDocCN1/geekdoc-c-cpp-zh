
![](img/ff0e6a9d867a3a6e9527eb1d946810fc_713_0.png)

# EXPERIMENT: Viewing the AppContainer table

An atom table is a hash table of integers to strings that's used by the windowing system for various identification purposes, such as Window Class registration (RegisterClassEx) and custom Windows messages. The AppContainer private atom can be viewed with the kernel debugger:

1. Run Calculator, open WinDbg, and start local kernel debugging.
2. Find the calculator:
```
kd>!process 1 calculator.exe
PROCESS fffff828cc9ed1080
SessionId: 1 Cid: 4b8d Peb: d040bbc000 ParentId: 03a4
DeepFreeze
DataBase: 5fccaaa00 ObjectTable: fffff950ad9fa2800 HandleCount:\Data Not Accessible
Image: Calculator.exe
VadRoot fffff82cd2c9b6a0 Vads 168 Clone 0 Private 2938. Modified 3332.
Locked 0:
DeviceMap fffff950ad2cd2f0
Token
...
ffff950adb313060
```

3. Use the token value with the following expressions:
```
kd> ?@st1 = @st0->NumberOfBuckets
kd> ?@st0 = (!@RTL_ATOM_TABLE*)((nt!_token)*0ffff950adb313060)-LowNumberEntry->AtomTable
kd> .for (@st3 = 0; @st3 < @st1; @st3 = @st3 + 1) { ?? (wchar*)@st0- 
Buckets (@s[3])->Name )
char_t = 0xffff950a*ac39b78a
"Protocols"
char_t = 0xffff950a*ac17b7aa
"Topics"
char_t = 0xffff950a*b2fd2822a
"TaskbarDPI_Desktop"
char_t = 0xffff950a*b3e2b47a
"Static"
char_t = 0xffff950a*b3c9458a
"TreeView"
char_t = 0xffff950a*ac34143a
"UserSubclassInfo"
char_t = 0xffff950a*ac552f0a
"StdShowItem"
char_t = 0xffff950a*abc6762a
"SysSetRedraw"
char_t = 0xffff950a*b4a5340a
"UIA_WindowVisibilityOverridden"
char_t = 0xffff950a*ab2c536a
"True"
...
char_t = 0xffff950a*b492c32ea
"tooltiptips_class"
char_t = 0xffff950a*ac23f46a
"Save"
char_t = 0xffff950a*ac29568a
"MSDraw"
char_t = 0xffff950a*ac54f32a
"StdNewDocument"
char_t = 0xffff950a*b546127a
"{F8B2E359-B442-4B58-9128-2319B8F3DE30}"
char_t = 0xffff950a*ac2e6f4a
"Status"
char_t = 0xffff950a*ad94265a
"Theme"
char_t = 0xffff950a*b3edfba
"Edit"
char_t = 0xffff950a*ab02e32a
"System"
char_t = 0xffff950a*b3ec53a
"MClient"
char_t = 0xffff950a*ac176ca
"StdName"
char_t = 0xffff950a*ac6bee6
"Exit"
char_t = 0xffff950a*b03c70a
"{C56C5799-48D3-4FAE-7FAD-DB2F6A53EF5}"
char_t = 0xffff950a*ab0360fa
"TabletService"
char_t = 0xffff950a*ac2ffea
"OLE"
```

## AppContainer capabilities

As you just saw, UWP applications have restricted rights. So, for example, is the Microsoft Edge application able to parse the local system and open PDF files in the user's folder? Similarly, how can the Music application play MP3 files directly through kernel access or by brokers (which you'll see in the next section)? The key lies in capability SIDs. Let's see where these come from, how they are used for. First, developers begin by creating an application manifest that specifies many details of their application such as the package name, resources, and more. One of the keys for capability management is the list of capabilities in the manifest. For example, let's look at Cortana's application manifest, located in `%SystemRoot%\SystemApps\Windows.Cortana_AppManifest.xml`.

```xml
<Capabilities>
<!-- for resolving -->
<Capability Name="settings" />
<Capability Name="cloudStore" />
<Capability Name="visualElements" />
<Capability Name="internetClient" />
<Capability Name="internetNetworkServer" />
<Capability Name="privateNetworkClient" />
<Capability Name="enterpriseAuthentication" />
<Capability Name="musicLibrary" />
<Capability Name="phoneCall" />
<Capability Name="picturesLibrary" />
<Capability Name="sharedCertificates" />
<Capability Name="locationHistory" />
<Capability Name="userDataSystem" />
<Capability Name="phoneCallHistory" />
<Capability Name="appointmentSystem" />
<Capability Name="chatSystem" />
<Capability Name="smsSend" />
<Capability Name="emailSystem" />
<Capability Name="packageQuery" />
<Capability Name="licenseValue" />
<Capability Name="secondaryAuthenticationFactor" />
<DeviceCapability Name="microphone" />
<DeviceCapability Name="location" />
<DeviceCapability Name="wifiControl" />
</Capabilities>
```

You'll see many types of entries in this list. For example, the Capability entries contain well-known SIDs associated with the original capability set that was implemented in Windows 8. These begin with `SECURITY_CAPABILITY_`—for example `SECURITY_CAPABILITY_INTERNET_CLIENT`, which is part of the capability under the APPLICATION AUTHORITY. This gives us a SID of S-1-15-3 in string format.

Other entries are prefixed with `uap`, `rescap`, and `wcap`. One of these (rescap) refers to capabilities that require special onboarding from Microsoft and custom approvals before being allowed on the store. In Cortana's case, these include capabilities such as accessing SMS messages, emails, location, and user data. Windows capabilities, on the other hand, refer to capabilities that are reserved for Windows and system applications. No store application can use these. UAP capabilities refer to standard capabilities that anyone can request on the store (Recall that UAP is the old name for UWP).

Unlike the first set of capabilities, which map to hard-coded RIDs, these capabilities are implemented in a different fashion. This uses a list of well-known RIDs to be constantly maintained. Instead, with this mode, capabilities can be fully updated and customized on the fly. To do this, they simply take the capability string, convert it to upper-case format, and take a SHA-2 hash of the resulting string, like AppContainer package SIDs are the SHA-2 hash of the package marker. Again, SHA-2 hashes are 32 bytes, this results in 8 RIDs for each capability, following the well-known `SECURITY_CAPABILITY_RID`.

Finally, you'll need a device ID. These refer to device classes that the UWP application will need to access, and can be identified through well-known strings as the ones you see above or by a GUID that identifies the device class. Rather than using one of the two methods of SID creation already described, one uses a third: for types of capabilities, the GUID is converted into a binary format and mapped out into four RID (because a GUID is 16 bytes). On the other hand, if a well-known name was specified, it must first be converted to a GUID. This is done by looking at the `HKLM\Software\Windows\Access\Mappings` registry key, which contains a list of registry keys associated with device capabilities and a list of GUIDs that map to these capabilities. The GUIDs are converted to a SID as you've seen.

> Note: For an up-to-date list of supported capabilities, see https://msdn.microsoft.com/en-us/windows/uwp/packaging/app-capability-declarations.

As encoding of all these capabilities into the token, two additional rules are applied:

- As you may have seen in the earlier experiment, each AppContainer token contains its own package SID as a capability. This can be used by the capability system to specifically lock down access to a particular app through a common security check instead of validating the package SID separately.
- Each capability is re-encoded as a group RID through the use of the `SECURITY_CAPABILITY_APPRID (1024)` RID as an additional sub-authority preceding the eight-capability hash RIDs.

After the capabilities are encoded into the token, various components of the system will read them to determine whether an operation being performed by an AppContainer should be permitted. You'll note most of the APIs are undocumented, as are left to broker services, inbox drivers, or kernel components. For example, the kernel and drivers can use the Rt1Capability API to authenticate access to hardware interfaces.

700 CHAPTER 7 Security
