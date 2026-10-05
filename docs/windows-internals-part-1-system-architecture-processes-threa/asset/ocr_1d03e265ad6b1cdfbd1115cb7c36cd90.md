(Peauth.sys), will recognize and report such attempts. Even on 32-bit systems, the driver has to be recognized by PMP policy or the playback may be halted. This policy is implemented by Microsoft and not by any kernel detection. This block would require manual action from Microsoft to identify the signature as malicious and update the kernel.

# Protected Process Light (PPL)

As we just saw, the original model for protected processes focused on DRM-protected content. Starting with Windows 8.1 and Windows Server 2012 R2, an extension to the protected process model was intro-duced, called Protected Process Light (PPL).

PPLs are protected in the same sense as classic processes: User-mode (even running with elevated privileges) cannot penetrate these processes by injecting threads or obtaining detailed information about loaded DLLs. However, the PPL model adds an additional dimension to the quality of being protected: attribute values. The different Signers have trust levels, which in turn results certain PPLs being more, or less, than other PPLs.

Because DRM evolved from multimedia DRM to Windows licensing DRM and Windows Store DRM, standard protected processes are also differentiated based on the Signer value. Finally, the various recognized Signers also define which rights are denied to lesser protected processes. For example, the only access masks allowed are PROCESS_QUERY/SET_LIMITED_INFORMATION AND PROCESS_SUSPEND_PROCESS_TERMINATE is not allowed for PPL signers.

Table 3-1 shows the legal values for the process flag stored in the EPROCESS structure.

| Internal Process Level Symbol | Protection Type | Signer |
|---|---||
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

As shown in Table 3-1, there are several signers defined, from high to low priority. WinSystem is the highest-priority signer used for the System process and minimal processes such as the Memory Compression process. For user-mode processes, WinTCB (Windows Trusted Computer Base) is the highest-priority signer leveraged to protect critical processes that the kernel has intimate knowledge

TABLE 3-1 Valid protection values for processes