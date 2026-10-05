
in the ability for this application to close the handles from underneath the AppContainer application. Even without malicious intent, the original launching application might exit, cleaning up its handles and destroying the AppContainer-specific object directory. To avoid this situation, AppContainer tokens have the ability to store an array of handles that are guaranteed to exist throughout the lifetime of any application using them. These handles are initially passed when the AppContainer token is being created (through NtCreateLowListBox) and are duplicated as kernel handles.

Similar to the AppContainer token, a special SEP_CACHED_HANDLES_ENTRY structure is used, this based on a hash table that's stored in the logon session for this user. (See "Logon" section in this chapter for more information on logon sessions.) This structure contains an array of kernel handles that have been duplicated during the creation of the AppContainer token. This will be closed either when this token is destroyed (because the application is exiting) or when the user logs off (which will result in tearing down the logon session).

## EXPERIMENT: Viewing token stored handles

To view token stored handles, follow these steps:

- 1. Run Calculator and launch local kernel debugging.
- 2. Search for the calculator process:

```
ikd>!process 0 1 calculator.exe
PROCESS fffff82c9d1080
SessionId: 1 Cid: 4bd8 Peb: d40bcb000 ParentId: 03a4
DeepFreeze
Base: 5ffca000 ObjectTable: fffff90ad9fa2800 HandleCount:
<Data Not Accessible>
Image: Calculator.exe
Vadroot fffff82cd2c9b6a0 Vads 168 Clone 0 Private 2938, Modified 3332.
Locked 0.
DeviceMap fffff90ad2cd2f0
Token fffff90ad513060
ElapsedTime 1 Day 08:01:47.018
UserTime 00:00:00.015
KernelTime 00:00:00.031
QuotaUsage[PagedPool] 465880
QuotaUsage[NonPagedPool] 23288
Working Sets (now,min,max) (7434, 50, 345) (29736KB, 200KB, 13800KB)
PeakWorkingSetSize 11097
VirtualSize 303 Mb
PeakVirtualSize 314 Mb
PageFaultCount 21281
MemoryPriority BACKGROUND
BasePriority 8
CommitCharge 4925
Job fffff828cd4914060
```

- 3. Dump the token using the dt command. (Remember to lower the mask 3 or 4 bits if they are not zero).

```
nkd> dt ntl_token fffff950adb31060
+0000 TokenSource : :TOKEN_SOURCE
+0010 TokenId : :LUID
+0018 AuthenticationId : :LUID
+0020 ParentTokenId : :LUID

+00c8 TokenFlags : 0x4a00
+00cc TokenInUse : 0x1
+00d4 IntegrityLevel : 1
+00d4 MandatoryPolicy : 1
+00d8 LogonSession : 0ffff950a'b4bb35c0_SEP_LOGON_SESSION_REFERENCES
+00e0 OriginatingLogonSession : :LUID
+00e8 SIdHash : :SID_AND_ATTRIBUTES
+01f8 RetainedSIdHash : :SID_AND_ATTRIBUTES
+0308 SecurityAttributes : 0ffff950a'e4f5f7f0_AUTHZBASED_SECURITY_nnATTRIBUTES_INFORMATION
+0310 Package : 0ffff950a'e0e0d6d0 Void
+0318 Capabilities : 0ffff950a'e8efb8c0_SID_AND_ATTRIBUTES
+0320 CapabilityCount : 1
+0328 CapabilitiesHash : :SID_AND_ATTRIBUTES
+0438 LowboxNumberEntry : 0ffff950a'b3fd5d50_SEP_LOWBOX_NUMBER_ENTRY
+0440 LowboxHandlesEntry : 0ffff950a'e6f91d90_SEP_LOWBOX_HANDLES_ENTRY
+0448 PClaimAttributes : (null)
```

- 4. Dump the LowboxHandlesEntry member:

```
kd> dt ntl_sep_lowbox_handles_entry 0ffff950a'e6f91d90
+0000 HashEntry : :RTL_DYNAMIC_HASH_ENTRY
+0018 ReferenceCount : On10
+0020 PackageSize : 0ffff950a'e6f9208 Void
+0028 HandleCount : 6
+0030 Handles : 0ffff950a'e9d18490 -> 0xffffff800023cc Void
```

- 5. There are six handles. Let's dump their values:

```
kd> dq fffff950ae9d18490 6
ffff950a'e9d18490 fffffffff0023cc fffffffff001e80
ffff950a'e9d18a0 fffffffff004214 fffffffff00425c
ffff950a'e9d18b0 fffffffff0002c fffffffff001834
```

- 6. You can see that these handles are kernel handles—values starting with 0xffffff64. Now you can use the !handle command to look at individual handles. Here are two examples from the six:

```
kd> !handle fffff8001e80
PROCESS fffff28cd71b360
Session: 1 Id: 2c74 Peb: 3df2f00 ParentId: 2324
DirBase: 80bb8500 ObjectTable: ffff50addab7c0 HandleCount: <Data Not Accessible>
Image: windbg.exe

kd> !handle fffff80002c8
PROCESS fffff28cd7b1360
SessionId: 1 Id: 27c4 Peb: 3df2fb00 ParentId: 2324
DirBase: 80bb8500 ObjectTable: ffff50addab7c0 HandleCount: <Data Not Accessible>
Image: windbg.exe
```

| Hash Address | Type | Name |
| --- | --- | --- |
| 23 | fffff82cb66e950 | ALPC Port |
| 376512899CCA5DE208534732 | SymbolicLink | Sessions\1\AppContainerNamedObjects\S-1-15-46627634-3793614953-270083692-180164423-2247275065-108783335-24683617* |

Finally, the ability to restrict objects to a particular directory namespace is a valuable security tool for sandboxing object access. The upcoming (at the time of this writing) Windows 10 Updates include an additional token capability called BNO isolation (where BNO refers to BaseNamedObjects). Using the SEP_CACHE_HANDLES_ENTRY structure, a new field, BnoIsolationHandlesEntry, is added to the TOKEN structure, with the type set to SepCachedEntryNoIsolation instead of SepCachedEntryLowbox. To use this feature, a special process attribute must be used (see Chapter 3 for more information), which contains an isolation prefix and a list of handles. At this point, the Lowbox mechanism is used, but instead of AppContainer SID object directory, with the prefix indicated in the attribute is used.

## Brokers

AppContainer processes have almost no permissions except for those implicitly granted with capabilities; some common operations cannot be performed by the AppContainer and require help. (There are also too level to be visible to users in the store, and difficult to manage.) Some examples include selecting files using the common Open dialog box or printing a Print dialog; for these and other operations, Windows provides helper processes, called brokers, managed by the system process, RuntimeBroker.exe.

An AppContainer requires that any of these communicates with the Runtime Broker through a secure ALPC channel and Runtime Broker initiates the creation of the requested broker process. Examples are %SystemRoot%\PrintDialog\PrintDialog.exe and %SystemRoot%\System32\PickerHost.exe.

## EXPERIMENT: Brokers

The following steps show how broker processes are launched and terminated:

- 1. Click the Start button, type Photos, and select the Photos to run the built-in Windows 10 Photos application.
- 2. Open Process Explorer, switch the process to Photos, and locate the broker process.
- 3. In the Photos app, select a file, right-click the menu and choose Print. The dialog box should open. ```
kd> !handle fffff8001e80
PROCESS fffff28cd71b360
Session: 1 Id: 2c74 Peb: 3df2f00 ParentId: 2324
DirBase: 80bb8500 ObjectTable: ffff50addab7c0 HandleCount: <Data Not Accessible>
Image: windbg.exe

- 4. Click the Print dialog box.

CHAPTER 7 Security

## Logon

Interactive logon (as opposed to network logon) occurs through the following:

- The logon process (Winlogon.exe)
- The user interface process (LogonUI.exe)
- Lsass.exe
- One or more authentication packages

Authentication packages are DLLs that perform authentication checks. Kerberos is the Windows authentication package for interactive logon to a domain. MSV1_0 is the Windows authentication package for interactive logon to a local computer, and when no domain controller is accessible.

Winlogon is a trusted process responsible for managing security-related interactions. It coordinates logon, starts the user's first process at logon, and handles logoff. It manages various operations relevant to security, including launching Winon for entering passwords, changing passwords, and locking and unlocking the workstation. Winlogon must ensure that operations relevant to security aren't visible to any active processes. For example, Winlogon guarantees that an untrusted process cannot control the desktop during one of these operations and thus gain access to the password.

Winlogon relies on the credential providers installed on the system to authenticate a user's account name or password. Credential providers are objects located inside DLLs. The default providers are authui, SmartCredentialProvider.dll, and FaceCredentialProvider.dll, which support password, smartcard PIN, and face-recognition authentication, respectively. Allowing other credential providers to be installed enables Windows to use different user-identification methods. For example, a third party may provide a credential provider that uses a fingerprint-recognition device to identify users and extract their passwords from an encrypted database.

To protect Winlogon's address space from bugs in credential providers that might cause the Winon process to crash (which, in turn, will result in a system crash, because Winlogon is considered a critical system process), a separate process, LogonUI.exe, is used to actually load the credential providers and display the Windows logon interface to. This process is started on demand when Winlogon needs to present a user interface to the user, and it exits after the action has finished. It also allows Winlogon to restart a new Logon process if it should crash for any reason.

Winlogon is the only process that intercepts logon requests from the keyboard. These are sent through an RPC message from Win32k.sys. Winlogon immediately launches the LogonUI application to
