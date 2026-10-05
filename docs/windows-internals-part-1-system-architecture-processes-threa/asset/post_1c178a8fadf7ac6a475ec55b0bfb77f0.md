
Restricted tokens are useful when an application wants to impersonate a client at a reduced security level, primarily for safety reasons when running untrusted code. For example, the restricted token can have the shutdown-system privilege removed from it to prevent code executed in the restricted token's security context from rebooting the system.

## Filtered admin token

As you saw earlier, restricted tokens are also used by UAC to create the filtered admin token that all user applications inherit. A filtered admin token has the following characteristics:

- The integrity level is set to medium.
- The administrator and administrator-SIDs mentioned previously are marked as deny-only to prevent a security hole if the group were to be removed altogether. For example, if a file has an access control list (ACL) that denied the Administrators group all access but granted some to another group the user belongs to, the user would be granted access if the Administrators group was absent from the token, which would give the standard user version of the user's identity more access than the administrator's identity.
- All privileges are stripped except Change, Notify, Shutdown, Undock, Increase Working Set, and Time Zone.

## EXPERIMENT: Looking at filtered admin tokens

You can make Explorer launch a process with either the standard user token or the administrator token by following these steps on a machine with UAC enabled:

- 1. Log on to an account that's a member of the Administrators group.
- 2. Open the Start menu, type command, right-click the Command Prompt option that appears, and choose Run as Administrator to run an elevated command prompt.
- 3. Run a new instance of cmd.exe, but this does not it normally (that is, not elevated).
- 4. Run Process Explorer elevated, open the Properties dialog boxes for the two command prompt processes, and click the Security tabs. Note that the standard token contains a deny-only SID and a medium mandatory label, and that it has only a couple of privileges. The properties on the right in the following screenshot are from a command prompt running with an administrator token, and the properties on the left are from one running with the filtered administrator token:

## Virtual service accounts

Windows provides a specialized type of account known as a **virtual service account** (or simply virtual account) to improve the security isolation and access control of Windows services with minimal administrative effort. (See Chapter 9 in Part 2 for more information on Windows services.) Without this mechanism, Windows services must run under one of the accounts defined by Windows for its built-in services (such as Local Service or Network Service) or a regular domain account. The accounts such as Local Service are shared by many services and have so limited granularity for privilege and access control; they cannot be managed across the domain. Domain accounts require periodic password changes for security, and the availability of services during a password-change cycle might be affected. Furthermore, for best isolation, each service should run under its own account, with ordinary accounts which only multiplies the management.

With virtual service accounts, each service runs under its own account with its own security ID. The name of the account is always NT SERVICE, followed by the internal name of the service. Virtual service accounts can appear in access control lists and can be associated with privileges via Group Policy like any other account. They cannot, however, be created or deleted through the usual management tools, nor assigned to groups.

Windows automatically sets and periodically changes the password of the virtual service account. Similar to the Local System and Other Service Accounts, there is a password, but the password is unknown to the system administrators.

## EXPERIMENT: Using virtual service accounts

You can create a service that runs under a virtual service account using the Service Control (Sc.exe) tool. Follow these steps:

- 1. In an Administrator command prompt, type the **create** command in the Sc.exe line to create a service and a virtual account in which it will run. This example uses the srvany service from the Windows 2003 resource kit, which you can download here: https://www.microsoft.com/en-us/download/details.aspx?id=17657.

```
C:\Windows\system32\sc create srvany obj="NT SERVICE\srvany" binPath="C:\temp\srvany.exe"
[SC] CreateService SUCCESS
```

- 2. The previous command created the service (in the registry and in the service controller manager's internal) and created the virtual service account snap (services.msc), select the new service, and open its Properties dialog box.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_663_0.png)

- 3. Click the **Log On** tab.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_663_1.png)

- 4. You can use the Services dialog box to create a virtual service account for an existing service. To do so, change the account name to NT SERVICE\servicename in The Account tab and clear password fields. Note, however, that services might not run correctly under a virtual service account because the account might not have access to files or other resources needed by the service.

- 5. If you run Process Explorer and view the Security tab in the Properties dialog box for a service that uses a virtual account, you can observe the virtual account name and its security ID (SID). To try this, in the Properties dialog box of the srvany service, the command-line arguments notepad.exe (srvany can be used to turn normal executables into services, so it must accept the.) Then click the Start to begin.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_664_0.png)

- 6. The virtual service account can appear in access control entry for any object (such as a file). If you click the Security tab in a Properties box and create an ACL that references the service name (for example, NT SERVICE\srvany) it appears in the access control list in shown format.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_665_0.png)

- 7. The virtual service account can be granted permissions (or user rights) via Group Policy. In this example, the srvany service has been granted the right to create a pagefile (using the Local Security Policy editor, secpol.msc).

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_665_1.png)

- 8. You won't see the virtual service account in user-administration tools like lusmgr.msc because it is not stored in the SAM registry hive. However, if you examine the registry within the context of the built-in System account (as described previously), you will see evidence of the account in the HKLM\System\Policy\Secrets keys:

```
C:\psec -s -d regedit.exe
```

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_666_0.png)
