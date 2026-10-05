
# Security identifiers

Instead of using names (which might or not be unique) to identify entities that perform actions in a system, Windows uses security identifiers (SIDs). Users have SIDs, as do local and domain groups, local computers, domain members, and services. A SID is a variable-length numeric value that consists of a SID structure revision number, a 48-bit identifier value, and a variable number of 32-bit subauthority or relative identifier (RID) values. The authority value identifies the agent that issued the SID, and this agent is typically a Windows local system or domain. Subauthority identify trustees to the issuing authority, and RIDs are a simple way for Windows to create unique SIDs based on a common base SID. Because SIDs are long and Windows takes time to generate truly random values within each SID, it is virtually impossible for Windows to issue the same SID twice on machines or domains anywhere in the world.

When displayed textualy, each SID carries a prefix, and its various components are separated with hyphens like so:

```
S-1-5-21-1463437245-122412800-86342198-1128
```

In this SID, the revision number is 1, the authority value is 5 (the Windows security authority), and four subauthority plus one RID (1128) make the remainder of the SID. This SID is a domain SID, but a local computer on the domain would have a SID with the same revision number, identifier authority value, and number of subauthority.

When you install Windows, the Windows Setup program issues the computer SID. Windows assigns local-account SIDs to accounts based on the source computer's SID and has a RID at the end. RIDs for accounts and groups start at 1000 and increase in increments of 1 for each new user or group. Similarly, Domain Controller Promote (Dcpromo.exe), the utility to create a new Windows domain, reuses the computer SID of the being promoted to domain controller and creates a new SID for the computer if it is demoted. Windows issues to new domain accounts SID that are based on the domain SID and have an appended RID (starting at 1000 and increasing in increments of 1 for each new user or group). A RID of 1028 indicates that the SID is the twenty-ninth SID inside the domain.

Windows issues SIDs that consist of a computer or domain SID with a predefined RID to many defined accounts and groups. For example, the RID for the Administrator account is 500, and the RID for the guest account is S001. A computer's local Administrator account, for example, has the computer SID as its base with the RID of 500 appended to:

```
S-1-5-21-13124455-12541255-62235125-500
```

Windows also defines a number of built-in local and domain SIDs to represent well-known groups. For example, a SID that identifies all and accounts (except anonymous users) is the Everyone SID: S-1-1-0. Another example of a group that a SID can represent is the Network group, which is the group that represents users who have logged on to a machine from the network. The Network group SID is S-1-5-2. Table 7-2, reproduced from the Windows SDK documentation, shows some basic SIDs, their numeric values, and their use. Unlike users' SIDs, these SIDs are predefined constants, and have the same values on every Windows system and domain in the world, is accessible by members of the Everyone group the system where it was created is also accessible to everyone on any other system or domain to which the hard drive it resides happens to be moved. Users on those systems, of course, authenticate to an account on those systems before becoming members of the Everyone group.

# TABLE 7-2 A few well-known SIDs

| SID | Name | Use |
|---|---|---|
| S-1-0-0 | Nobody | Used when the SID is unknown |
| S-1-1-0 | Everyone | A group that includes all users except anonymous users |
| S-1-2-0 | Local | Users who log on terminals (physically) connected to the system |
| S-1-3-0 | Creator Owner ID | A security identifier to be replaced by the security identifier of the user who created a new object (in inheritable ACEs) |
| S-1-3-1 | Creator Group ID | Identifies a security identifier to be replaced by the Primary group SID of the user who created a new object (in inheritable ACEs) |
| S-1-5-18 | Local System account | Used by services |
| S-1-5-19 | Local Service account | Used by services |
| S-1-5-20 | Network Service account | Used by services |

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_642_0.png)

> Note See Microsoft Knowledge Base article 243330 for a list of defined SIDs at http://support.microsoft.com/kb/243330.

Finally, Winlogin creates a unique logon SID for each interactive logon. A typical use of a logon SID is in an access control entry (ACE) that allows access for the duration of a client's logon session. For example, a Windows service can use the LogonUser function to start a new logon session. The LogonUser returns an account token from which the service can extract the SID. The service can then use the SID in an ACE (described in the section "Security descriptors and access control" later in this chapter) that allows the client's logon session to access the interactive window station and desktop. The SID for a logon session is S-1-5-5-X-Y, where the X and Y are randomly generated.

> EXPERIMENT: Using PsGetSid and Process Explorer to view SIDs
You can see the SID representation for any account you're running by the PsGetSid utility from Sysinternals. PsGetSid's options allow you to translate and user account to their corresponding SIDs and vice versa.
If you run PsGetSid with no options, it prints the SID assigned to the local computer. Because the Administrator account always has a RID of 500, you can determine the name assigned to the account (in cases where a system administrator has renamed the account for security reasons) simply by passing the machine appended with -500 as PsGetSid's command-line argument.

To obtain the SID of a domain account, enter the user name with the domain as a prefix:

```
c:\>
```

# Integrity levels

As mentioned, Mandatory Integrity Control (MIC) allows to isolate code and data within a user. The integrity level of a token can be obtained with the GetTokenInformation API with the Token-IntegrityLevel value. These integrity levels are specified by a SID. Although integrity levels can be arbitrary values, the system uses primary levels to separate privilege, as described in Table 7-3.

# TABLE 7-3 Integrity levels

| SID | Name (Level) | Use |
|---|---|---|
| S-1-16-0000 | Untrusted (0) | Used by processes started by the Anonymous group. It blocks most access. |
| S-1-16-10000 | Low (1) | Used by AppContainers (UWP) and Protected Mode Internet Explorer. It blocks write to most objects (such as files and registry keys) on the system. |
| S-1-16-20000 | Medium (2) | Used by normal applications launched while UAC is enabled. |
| S-1-16-03000 | High (3) | Used by administrative applications launched through elevation when UAC is enabled, or normal applications if UAC is disabled and the user is an administrator. |
| S-1-16-04000 | System (4) | Used by services and other system-level processes (such as Wininit, Winlong, Smss, and on). |
| S-1-16-05000 | Protected (5) | Currently unused by default. Can be set by kernel-mode caller only. |

# EXPERIMENT: Looking at the integrity level of processes

You can use Process Explorer to quickly display the integrity level for the processes on your system. The following steps demonstrate this functionality.

+   1. Launch Microsoft Edge browser and Calc.exe.
2. Open an elevated command prompt window.
3. Open Notepad normally (without elevating).
4. Open an elevated Process Explorer, right-click any column header in the Process list, and then click Select Columns.
