
(Peauth.sys), will recognize and report such attempts. Even on 32-bit systems, the driver has to be recognized by PMP policy or the playback may be halted. This policy is implemented by Microsoft and not by any kernel detection. This block would require manual action from Microsoft to identify the signature as malicious and update the kernel.

## Protected Process Light (PPL)

As we just saw, the original model for protected processes focused on DRM-protected content. Starting with Windows 8.1 and Windows Server 2012 R2, an extension to the protected process model was introduced, called Protected Process Light (PPL).

PPLs are protected in the same sense as classic processes: User-mode (even running with elevated privileges) cannot penetrate these processes by injecting threads or obtaining detailed information about loaded DLLs. However, the PPL model adds an additional dimension to the quality of being protected: attribute values. The different Signers have trust levels, which in turn results certain PPLs being more, or less, than other PPLs.

Because DRM evolved from multimedia DRM to Windows licensing DRM and Windows Store DRM, standard protected processes are also differentiated based on the Signer value. Finally, the various recognized Signers also define which rights are denied to lesser protected processes. For example, the only access masks allowed are PROCESS_QUERY/SET_LIMITED_INFORMATION AND PROCESS_SUSPEND_PROCESS_TERMINATE is not allowed for PPL signers.

Table 3-1 shows the legal values for the process flag stored in the EPROCESS structure.

| Internal Process Level Symbol | Protection Type | Signer |
| --- | --- | --- |
| PS_PROTECTED_SYSTEM (0x72) | Protected | WinSystem |
| PS_PROTECTED_WINTCB (0x62) | Protected | WinTcb |
| PS_PROTECTED_WINTCB_LIGHT (0x61) | Protected Light | WinTcb |
| PS_PROTECTED_WINDOWS (0x52) | Protected | Windows |
| PS_PROTECTED_WINDOWS_LIGHT (0x51) | Protected Light | Windows |
| PS_PROTECTED_LSA (0x41) | Protected | Lsa |
| PS_PROTECTED_ANTIMALWARE_LIGHT (0x31) | Protected Light | Anti-malware |
| PS_PROTECTED_AUTHENTICATE (0x21) | Protected | Authentic |
| PS_PROTECTED_AUTHENTICATE_LIGHT (0x11) | Protected Light | Authentic |
| PS_PROTECTED_NONE (0x00) | None | None |

As shown in Table 3-1, there are several signers defined, from high to low priority. WinSystem is the highest-priority signer used for the System process and minimal processes such as the Memory Compression process. For user-mode processes, WinTCB (Windows Trusted Computer Base) is the highest-priority signer leveraged to protect critical processes that the kernel has intimate knowledge of and reduce its security boundary toward. When interpreting the power of a process, keep in mind that protected processes always trump PPLs, and that next, higher-value signers have access to lower ones, but not vice versa. Table 3-2 shows the signer levels (higher values denote the signer is more powerful) and some examples of their usage. You can also dump these in the debugger with the _PS_PROTECTED_SIGNER type.

TABLE 3-1 Valid protection values for processes

### TABLE 3-2 Signers and levels

| Signer Name (PS_PROTECTED_SIGNER) | Level | Used For |
| --- | --- | --- |
| PsProtectedSignWinSystem | 7 | System and minimal processes (including Pico processes). |
| PsProtectedSignWinTcb | 6 | Critical Windows components. PROCESS_TERMINATE is denied. |
| PsProtectedSignWindows | 5 | Important Windows components handling sensitive data. |
| PsProtectedSignLsa | 4 | Lsass.exe (if configured to run protected). |
| PsProtectedSignAntimalware | 3 | Anti-malware services and processes, including third party. PROCESS_TERMINATE is denied. |
| PsProtectedSignCodeGen | 2 | NGEN (NET native code generation). |
| PsProtectedSignAuthenticator | 1 | Hosting DRM content or using user-mode fonts. |
| PsProtectedSignNone | 0 | Not valid (protection). |

At this point you may be wondering what prohibits a malicious process from claiming it is a protected and shielding itself from anti-malware (AM) applications. Because the Windows Media DRM Certificate is no longer necessary to run as a protected process, Microsoft extended its Code Integrity module to understand two special enhanced key (EKU) OIDs for code signing certificate: 1.3.6.1.4.1.311.10.3.22 and 1.3.6.1.4.1.311.10.3.20. Once one of these EKUs is present, hardcoded Google and Issuer strings in the certificate, combined with additional possible EKUs, for example, the Microsoft Windows Issuer can grant the PsProtectedWindows protected signer value, but only if the EKU for Windows System Component Verification (1.3.6.1.4.1.311.10.3.6) is also present. As an example, Figure 3-7 shows the certificate for Smss.exe, which is permitted to run as WinTcb.

Finally, note that the protection level of a process also impacts how DLLs will be allowed to load—otherwise through a logic bug or simple file replacement or replacing, a legitimate process could be coerced into loading a third party or malicious library, which would now execute with the same protection level as the process. This is checked by granting each process a "Signature Level," which is stored in the SignerLevel field of EPROCESS, and using an internal lookup to find a corresponding "DLL Signature Level," stored in SectionSignatureLevel in EPROCESS. Any DLL loading in the process will be checked by the Code Integrity component in the same way that the main executable is verified. For example, a process with "WinTcb" as its executable signer will only load "Windows" or higher signed DLLs.

## CHAPTER 3 Processes and jobs

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_133_0.png)

**3-7** Smss certificate.

On Windows 10 and Windows Server 2016, the following processes are PPL signed with WinTcb-Lite: smss.exe, csrss.exe, and wininit.exe. Lass.exe is running as PPL on ARM-based Windows (such as Windows mobile 10) and can run as PPL on x86/x64 if configured as by a registry setting (see Chapter 7 for more information). Additionally, certain services are configured to run as PPL such as sppsvc.exe (Software Protection Platform). You may also notice certain service-hosting (svchost.exe) running with this protection level. More information on protected services will be described in Chapter 9. The fact that these core binaries are TCB is critical to the security of the system. For example, Csrss.exe has access to sensitive parts of the kernel implemented by the Windows Manager (Win32k.sys), which could give an attacker Administrator rights.

| Process Name | Minimum Signature Level | Minimum Protection Level |
| --- | --- | --- |
| Smss.exe | Inferred from protection level | WinTcb-Lite |
| Csrss.exe | Inferred from protection level | WinTcb-Lite |
| Wininit.exe | Inferred from protection level | WinTcb-Lite |
| Services.exe | Inferred from protection level | WinTcb-Lite |
| Werfaultsecure.exe | Inferred from protection level | WinTcb-Full |
| Sppsvc.exe | Inferred from protection level | Windows-Full |
| Genvalobj.exe | Inferred from protection level | Windows-Full |
| Lass.exe | SE_SIGNING_LEVEL_WINDOWS | 0 |
| Userinit.exe | SE_SIGNING_LEVEL_WINDOWS | 0 |
| Winlogon.exe | SE_SIGNING_LEVEL_WINDOWS | 0 |
| Autoch.exe | SE_SIGNING_LEVEL_WINDOWS* | 0 |

*Only on UEFI firmware systems

TABLE 3-3 Minimum TCB
