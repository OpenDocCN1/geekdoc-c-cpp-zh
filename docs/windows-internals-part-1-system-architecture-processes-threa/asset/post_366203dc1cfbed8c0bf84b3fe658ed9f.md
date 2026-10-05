
## File virtualization

The system locations that are virtualized for legacy processes are %ProgramFiles%, %ProgramData%, and %SystemRoot%, excluding some specific subdirectories. However, any file with an executable extension—including .exe, .bat, .scr, .vbs, and others—is excluded from virtualization. This means programs that update themselves from a standard user account instead of creating private versions of their executables that are not visible to an administrator running a global update.

> Note To add extensions to the exception list, enter them in the HKLM\System\ControlSet\Services\Luaf\Parameters\ExcludedExtensions registry key and reboot. Use a multicast to delete multiple extensions, and do not include a leading dot extension name.

Modifications to virtualized directories by legacy processes are redirected to the user’s virtual root directory, %AppData%\VirtualStore. The Local component of the path highlights the fact that virtualized files do not run with the rest of the process when the account has a roaming profile.

The UAC File Virtualization filter driver (%SystemRoot%\System32\Drivers\luaf.sys) implements file virtualization. Because this is a file system filter driver, it sees all local file system operations, but it implements functionality only for operations from legacy processes. As shown in Figure 7-23, the filter driver changes the target file path for a legacy process that creates a file in a system-global location but not for a non-virtualized process with standard user rights. Default permissions prevent the directory access to the application written with UAC support, but the legacy process acts as though the operation succeeds when it really created the file in a location fully accessible by the user.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_741_0.png)

FIGURE 7-23 UAC File Virtualization filter driver operation.

## EXPERIMENT: File virtualization behavior

In this experiment, you will enable and disable virtualization on the command prompt and see several behaviors to demonstrate UAC file virtualization:

- 1. Open a non-elevated command prompt (you must have UAC enabled for this to work) and enable virtualization for it. You can change the virtualization status of a process by right-clicking the process in the Task Manager Details tab and selecting UAC Virtualization by the shortcut menu that appears.
- 2. Navigate to the C:\Windows directory and use the following command to write a file:
echo hello-1 > test.txt
- 3. List the contents of the directory. You will see that the file appears.
dir test.txt
- 4. Disable virtualization by right-clicking the process in the Task Manager Details tab and deselecting UAC Virtualization. Then list the directory as step 3. Notice that the file is gone, however, a directory listing of the VirtualStore will reveal the file:
d %local%
- 5. Enable virtualization for this process.
- 6. Look at a more complex scenario, create a new command prompt window, but elevated this time. Repeat steps 2 and 3 using the string hello-2.
- 7. Examine the text inside these files using the following command in both command prompts. The screenshots will show the expected output.
type test.txt

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_742_0.png)

```
Administrator Command Prompt
Microsoft Windows (Version 10.0.14393)
(C) 2016 Microsoft Corporation. All rights reserved.
C:\WINDOWS\system32>cd windows
C:\Windows>echo hello-2 > test.txt
C:\Windows>type test.txt
hello-2
C:\Windows>
```

- 8. From your elevated command prompt, delete the test.txt file:
del test.txt

- 9. Repeat step 3 of the experiment in both windows. Notice that the elevated command prompt cannot find the file anymore, while the standard user command prompt shows the old contents of the file again. This demonstrates the failure mechanism described earlier: Read operations lock in the per-user virtual store location first, but if the file doesn't exist, access to the system location will be granted.

## Registry virtualization

Registry virtualization is implemented slightly differently from file system virtualization. Virtualized registry keys include most of HKEY_LOCAL_MACHINE\branch, but there are numerous exceptions, such as the following:

- HKLM\Software\Microsoft\Windows
- HKLM\Software\Microsoft\Windows NT
- HKLM\Software\Classes

Only keys that are commonly modified by legacy applications, that don't introduce compatibility or interoperability problems, are virtualized. Windows redirects modifications of virtualized keys by a legacy application to a user's registry root at HKLM\CURRENT_USER\Software\VirtualStore. The key is located in the user's Classes hive, %AppData%\Microsoft\Windows\UsrClass.dat, like other virtualized file data, does not roam with the roaming user profile. Instead of maintaining a fixed list of virtualized locations as Windows does for the file system, the virtualization status of a key is stored as a combination of flags, shown in Table 7-16.

You can use the Reg.exe utility in Windows, with the flags option, to display the current virtualization status for a key or to set it. In Figure 7-24, note that the HKLM\Software key is fully virtualized, but the Windows subkey (and all its children) have only silent failure enabled.

## TABLE 7-16 Registry virtualization flags

| Flag | Meaning |
| :--- | :--- |
| REG_KEY_DONT_VIRTUALIZE | This specifies whether virtualization is enabled. If this flag is set, virtualization is disabled. |
| REG_KEY_SILENT_FAIL | This specifies whether virtualization is granted. If this flag is set, it's denied. |
| REG_KEY_RECURSE_FLAG | This determines whether virtualization will propagate to child keys. |

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_744_0.png)

FIGURE 7-24 UAC virtualization flags.

## Elevation

Even if users run programs that are compatible with standard user rights, some operations still require administrative rights. For example, the vast majority of software installations require administrative rights to install services or device drivers. Modifying system-global settings also requires administrative rights, as do parental controls. It would be possible to perform most of these by switching to a administrator account, but the inconvenience of doing so would result in most members using the administrator account for their daily tasks.

It's important to be aware that UAC elevations are conveniences and not security boundaries. A security boundary requires that security policy dictate what can pass through. User accounts are an example of a security boundary because one user can't access the data belonging to another user without that user's permission.

Because elevations aren't security boundaries, there's no guarantee that malware running on a system with standard user rights can't compromise an elevated process to gain administrative rights. For example, elevation dialog boxes only identify what will be elevated; they say nothing about it when executes.

## Running with administrative rights

Windows includes enhanced "run as" functionality so that standard users can conveniently launch processes with administrative rights. This functionality giving applications a way to identify operations for which the system can obtain administrative rights on behalf of the application

To enable users acting as system administrators to have not enter names and passwords every time they want to access administrative rights, Windows makes use of a mechanism called Admin Approval Mode (AAM). This feature creates two identities for the user at logon: with standard user rights and other administrative rights. Since every user on a Windows system is either a standard user or acting for the most part as a standard user in AAM, developers must assume that all users are standard users, which will result in more programs working with standard user without virtualization or shims.

Granting administrative rights to a process is called elevation. When elevation is performed by a user account (or by a user who is part of an administrative group but not the actual Administrators group), it is referred to as over-the-shoulder (OTS) elevation because it requires the entry of credentials for an account that's a member of the Administrators group, something that is usually completed by a privileged user typing over the shoulder of a standard user. An elevation performed by an AAM user is called consent elevation because the user simply has to approve the assignment of his administrative rights.

Standalone systems, which are typically home computers, and domain-joined systems treat AAM access by remote users differently-domain-connected users can use administrative groups in their resource permissions. When a user accesses a stand-alone computer's file share,
