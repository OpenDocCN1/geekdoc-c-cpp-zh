# Tokens

The SRM uses an object called a token (or access token) to identify the security context of a process or thread. A security context contains information that describes the account, groups, and privileges asassociated with the process or thread. Tokens also include information such as the session ID, the integrity level, and the UAC virtualization state (We'll describe both privileges and UAC's virtualization mechanism later in this chapter).

During the login process (described later in this chapter), Lsass creates an initial token to represent the user logging on. It determines whether the user logging on is a member of a powerful group or possesses a powerful privilege. The groups checked for this step are as follows:

+   - Built-In Administrators
- Certificate Administrators
- Domain Administrators
- Enterprise Administrators
- Policy Administrators
- Schema Administrators
- Domain Controllers
- Enterprise Read-Only Domain Controllers
- Read-Only Domain Controllers
- Account Operators
- Backup Operators
- Cryptographic Operators
- Network Configuration Operators
- Print Operators
- System Operators
- RAS Servers
- Power Users
- Pre-Windows 2000 Compatible Access

Many of the groups listed are used only on domain-joined systems and don't give users local-administrative rights directly. Instead, they allow users to modify domain-wide settings.

The privileges checked for each are as follows:

+   - SeBackupPrivilege
- SeCreateTokenPrivilege
- SeDebugPrivilege
- SeImpersonatePrivilege