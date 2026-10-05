# Integrity levels

As mentioned, integrity levels can override discretionary access to differentiate a process and objects running as owned by the same user, offering the ability to isolate code and data within a user account. The mechanism of Mandatory Integrity Control (MIC) allows the SRM to have more detailed information about the nature of the caller by associating it with an integrity level. It also provides information on the trust required to access the object by defining an integrity level for it.

The integrity level of a token can be obtained with the GetTokenInformation API with the Token-IntegrityLevel enumeration value. These integrity levels are specified by a SID. Although integrity levels can be arbitrary values, the system uses primary levels to separate privilege, as described in Table 7-3.

# TABLE 7-3 Integrity levels

| SID | Name (Level) | Use |
|---|---|---|
| S-1-16-0xo | Untrusted (0) | Used by processes started by the Anonymous group. It blocks most access. |
| S-1-16-10000 | Low (1) | Used by AppContainers (UWP) and Protected Mode Internet Explorer. It blocks write to most objects (such as files and registry keys) on the system. |
| S-1-16-20000 | Medium (2) | Used by normal applications being launched while UAC is enabled. |
| S-1-16-03000 | High (3) | Used by administrative applications launched through elevation when UAC is enabled, or normal applications if UAC is disabled and the user is an administrator. |
| S-1-16-04000 | System (4) | Used by services and other system-level processes (such as Wininit, Winlong, Smss, and on). |
| S-1-16-05000 | Protected (5) | Currently unused by default. Can be set by kernel-mode caller only.

Another, seemingly additionally, integrity level is called AppContainer, used by UWP apps. Although seemingly another level, it's in fact equal to Low. UWP process tokens have another attribute that indicates they are running inside an AppContainer (described in the "AppContainers" section). This information is available with the GetTokenInformation API with the TokenIsAppContainer enumeration.

# EXPERIMENT: Looking at the integrity level of processes

You can use Process Explorer to quickly display the integrity level for the processes on your system. The following steps demonstrate this functionality.

+   1. Launch Microsoft Edge browser and Calc.exe (Windows 10).
2. Open an elevated command prompt window.
3. Open Notepad normally (without elevating).
4. Open an elevated Process Explorer, right-click any column header in the Process list, and then click Select Columns.