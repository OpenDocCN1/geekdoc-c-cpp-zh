8. You won't see the virtual service account in user-administration tools like lusmgr.msc because it is not stored in the SAM registry hive. However, if you examine the registry within the context of the built-in System account (as described previously), you will see evidence of the account in the HKLM\System\Policy\Secrets keys:

```
C:\psec -s -i -d regedit.exe
```

![](bbox=[0.198, 0.197, 0.802, 0.506])

# Security descriptors and access control

Tokens, which identify a user's credentials, are only part of the object security equation. Another part of the equation is the security information associated with an object, which specifies who can perform what actions on the object. The data structure for this information is called a security descriptor. A security descriptor contains the following attributes:

+   - **Revision number** This is the version of the SRM security model used to create the descriptor.
- **Flags** These are optional modifiers that define the behavior or characteristics of the descriptor. These flags are listed in Table 7-5 (most are documented in the Windows SDK).
- **Owner SID** This is the owner's SID.
- **Group SID** This is the SID of the primary group for the object (used only by the POSIX subsystem, now unused since POSIX is no longer supported).
- **Discretionary access control list (DACL)** This specifies who has access to the object.
- **System access control list (SACL)** This specifies operations by which users should be logged in the security audit audit log and the explicit integrity level of an object.

650 CHAPTER 7 Security