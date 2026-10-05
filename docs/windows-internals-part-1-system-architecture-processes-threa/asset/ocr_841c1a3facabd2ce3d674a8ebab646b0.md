# TABLE 7-11 Privileges (continued)

| Privilege | User Right | Privilege Usage |
| --- | --- | --- |
| SeTakeOwnershipPrivilege | Take ownership of files and other objects | Required to take ownership of an object without being granted discretionary access. |
| SecbPrivilege | Act as part of the operating system | Checked for the SRM when the session ID is set in a token, by the Plug and manager for Plug and Play event creation and management, by BroadcastSystemAgentsDESKTO, with LsaRegisterLoginProcess, and when specifying an application a VDM with NtSetInformationProcess. |
| SeTimeZonePrivilege | Change the time zone | Required to change the time zone. |
| SeTrustedCredAccessPrivilege | Access Credential Manager as a trusted caller | Checked by the Credential Manager to verify that it trusts the caller with credential information that can be queried in plaintext. It is granted only to Windows by. |
| SeUndockPrivilege | Remove computer from a docking station | Checked for the user-mode Plug and manager when either a computer undock is initiated or a device request is made. |
| SeUnsolicitedInputPrivilege | Receive unsolicited data from a terminal device | This privilege is not currently used by Windows.

When a component wants to check whether a privilege is present, the Privilege-Check or LsaEnumerateAccountRights APIs if running in user mode and SeSinglePrivilegeCheck SePrivilegeCheck if running in kernel mode. The privilege-related APIs are not account-aware, but the account-right APIs are privilege-aware.

Unlike account-rights, privileges can be enabled and disabled. For a privilege to succeed, the privilege must be in the specified token and must be enabled. The idea behind this scheme is that privileges should be enabled only when their use is required so that a process cannot inadvertently perform a privileged operation. Enabling or disabling privileges can be done with the AdjustTokenPrivileges function.

# EXPERIMENT: Seeing a privilege get enabled

By following these steps, you can see that the Date and Time Control Panel enables the SeTimeZonePrivilege privilege in response to using its interface to change the time zone of the computer (Windows 10):

+   1. Run Process Explorer.
2. Right-click the clock in the system tray in the taskbar and choose Adjust Date/Time. Alternatively, open the Settings app and search for time to open the Date and Time settings page.