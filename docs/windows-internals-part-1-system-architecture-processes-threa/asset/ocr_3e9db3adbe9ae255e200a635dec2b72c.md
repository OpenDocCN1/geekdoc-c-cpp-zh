AppL auditing mode can be used to monitor which applications are being used by one or more users on a system.

AppL allows an administrator to restrict the following types of files from being run:

+   - Executable images (EXE and COM)
- Dynamic-link libraries (DLL and OCX)
- Microsoft Software Installer (MSI and MSP) for both install and uninstall
- Scripts
- Windows PowerShell (PS1)
- Batch (BAT and CMD)
- VisualBasic Script (VBS)
- Java Script (JS)

AppLocker provides a simple GUI-based mechanism, which is very similar to network firewall rules, for determining which applications or scripts are allowed to run by specific users and groups, using conditional ACEs and AppID attributes. There are two types of rules in AppLocker:

+   - Allow the specified files to run, denying everything else.
- Deny the specified files from running, denying everything else. Deny rules take precedence over allow rules.

Each rule can also have a list of exceptions to exclude files from the rule. Using an exception, you could create a rule to, for example, allow everything in the C:\Windows or C:\Program directories to be except RegEdit.exe.

AppLocker rules can be associated with a specific user or group. This allows an administrator to support compliance by validating and enforcing which users can run specific applications. For example, you can create a rule to allow users in the Finance security group to run the finance-of-business applications. This blocks everyone who is not in the Finance security group from running finance applications (including administrators) but still provides access for those who have a business need to run the applications. Another useful rule would be to prevent users in the Receptionists group from installing or running unapproved software.

AppLocker rules can depend upon conditional ACEs and attributes defined by AppID. Rules can be created using the following criteria:

+   - Fields within a code-signing certificate embedded within the file, allowing for different combinations of publisher name, product name, file name, and version For example, a rule could be created to allow all versions greater than 9.0 of Contoso Reader to run or allow anyone in the group to run the installer or application from Contoso for GraphicsShop as long as the length is 14.* For example, the following SDDL string denies execute access to