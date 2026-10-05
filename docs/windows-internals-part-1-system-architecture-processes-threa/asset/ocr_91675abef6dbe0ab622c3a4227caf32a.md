# EXPERIMENT: Viewing service details inside processes

Process Explorer highlights processes hosting one or more. (These processes are shaded pink color by default, you can change this by using the **Options** menu and choosing **Configure Colors**. If you double-click a service-hosting process, you will see a Services tab that lists the inside process, the name of the registry key that defines the service, the display name seen by the administrator, the description text for that (if present), and for Svchost exe, the path to the DLL that implements the service. For example, listing the services in one of the Svchost processes running under the System account appears as follows:

![](bbox=[0.152, 0.253, 0.532, 0.563])

# Winlogon, LogonUI, and Userinit

The Windows logon process (%SystemRoot%\System32\Winlogon.exe) handles interactive user logons and logoffs. Winlogon.exe is notified of a user logon request when the user enters the attention sequence (SAS) keyboard combination. The default SAS on Windows is Ctrl+Alt+Delete. The reason for the SAS is to protect users from password-capture programs that simulate the logon process because this keyboard sequence cannot be intercepted by a user-mode application.

The identification and authentication aspects of the logon process are implemented through DLLs called **credential providers**. The standard credential providers implement the default Windows authentication interfaces: password and smartcard. Windows 10 provides a biometric provider: face recognition, known as **Hello**. However, developers can provide their own credential providers to implement other identification and authentication mechanisms instead of the Windows user name/password method, such as one based on a voice print or biometric device such as a fingerprint reader. Because Winlogon.exe is a critical system process on which the system depends, credential providers and the UI to display the logon dialog box run inside a child process of Winlogon.exe

CHAPTER 2 **System architecture**