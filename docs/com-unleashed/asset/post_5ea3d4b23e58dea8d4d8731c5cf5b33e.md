
## CHAPTER 12

## COM Security

### IN THIS CHAPTER

- COM Versus DCOM Security 298
- Windows Security 299
- Impersonation 314
- Declarative Security 319
- Programmatic Security 319

### COM Versus DCOM Security

This chapter examines how to work with COM+ security in order to allow and deny access to a COM+ server. I’m covering plain vanilla COM security in this chapter because it’s an important topic to master before some of the distributed topics are addressed (especially MTS and Transactions). Later, in chapter 18, “COM+ Security,” the COM+-specific security issues are covered.

Before the release of DCOM, object security was not an important issue. Because objects could not access objects across the network, you only had to worry about objects on the same machine. Controlling objects on one machine is fairly easy, but managing them across a 200-workstation network is slightly more difficult than rocket science, unless you have built-in security as provided by DCOM.

A common misunderstanding is that DCOM provides security and that COM does not provide security. This is incorrect because the security added with the release of DCOM applies just as equally to legacy COM objects, distributed COM (DCOM) objects, and non-distributed COM objects. It is possible to disable distributed COM and enable COM objects to use the DCOM security. The DCOM security and distributed objects can be used independently of each other.

I use COM security and DCOM security as synonyms. They are in fact the same. When I refer to COM security prior to the introduction of DCOM security, I say exactly that, “COM security prior to DCOM.” In order to understand that DCOM security and COM security are one and the same, think of the DCOM package as having introduced two subsystems to COM: a remoting subsystem and a security subsystem.

### COM Security and SSPI

COM implements security using Microsoft’s Security Support Provider Interface (SSPI). This enables COM to use any security provider that exposes itself with the SSPI interface. At this point, you might be asking, “Why doesn’t COM just access the security protocol directly?” Microsoft’s long-term strategy is to make COM available across a variety of platforms, including platforms that do not implement security, such as Macintosh and UNIX.

Another important reason why COM doesn’t access security protocol directly is that COM is really just an object-oriented version of DCE RPC (Distributed Computing Environment Remote Procedure Call). DCE RPC is also designed in such a manner that it can take advantage of a variety of security providers.

Security, more appropriately called NT LAN Manager Security Service Provider (NTLMSSP), was the first security provider that exposed itself using an SSPI interface. The NTLMSSP provider is available on all NT workstations and servers and is, therefore, the primary candidate (and sometimes the only candidate) available for use with DCOM security. In order to continue the discussion of DCOM security, you begin by learning the security fundamentals.

The default protocol for network authentication in Windows 2000 is the Kerberos v5 authentication protocol. An emerging authentication standard, the Kerberos protocol provides a foundation for interoperability. It also enhances the security of enterprise-wide network authentication. Key components of the protocol’s implementation in Windows 2000 include the following:

- Integration of initial authentication with the Winlogon single sign-on architecture.
- Use of Active Directory, the directory service included in Windows 2000, in the Windows 2000 domain as a domain’s security account database.
- Implementation of the Kerberos client as a Windows 2000 security provider through the Security Support Provider Interface (SSPI).

### Windows Security

Windows provides security to a variety of object types: files, devices, processes, threads, semaphores, shared memory, registry keys, and more. In order to implement this security, every newly made object is created with a security descriptor. It would be very difficult to manage every object over every NT workstation, so NT simplifies security by dividing NT workstations into domains.

The combination of Owner (owning SID), list of principals (DACL), and list of principals to audit (SACL) is called a security descriptor (SD). A security descriptor completely describes the security policy in terms of object owner, access, and auditing. The security descriptor (in its self-relative form) is a memory structure that references its elements (DACL, SACL, and so on) using offsets instead of pointers. This self-relative security descriptor can thus simply be written into a registry key and safely retrieved.

### Developing Security with Domains

You can think of a domain as a group of networked machines. In the group of networked machines, one machine is nominated as the primary domain controller. This is the centrally managed authentication controller that authenticates access to networked resources.

Multiple domains can exist in a trust relationship. That is, if a security principal cannot be authenticated within a domain, the primary domain controller can attempt to authenticate the security principal against a trusted domain. This enables large network configurations to be managed on a smaller scale, with smaller domain configurations.

Providing an authentication authority with the user identification and password confirms secured network access. Unless the authentication authority is specified, the network access will be verified using the local registration database and the domain registration database.

### Security Descriptors

As mentioned earlier in this section, every newly made securable object is created with a security descriptor. The security descriptor is made up of two security IDs (SIDs) and two access control lists (ACLs). The two SIDs represent the securable object's owner and owner group. The two ACLs are the discretionary access control list (DACL) and the system access control list (SACL). You learn about ACLs, DACLs, and SACLs in more detail later in this chapter.

When you create a new securable object in NT, you should pass a SECURITY_ATTRIBUTES structure to the object. The SECURITY_ATTRIBUTES contains the SECURITY_DESCRIPTOR structure. The definition of both these structures is shown in Listing 12.1.

### LISTING 12.1 SECURITY_ATTRIBUTES and SECURITY_DESCRIPTOR Definitions

```c
typedef struct _SECURITY_ATTRIBUTES
{
    DWORD nLength;
    LPVOID lpSecurityDescriptor;
    BOOL bInheritHandle;
} SECURITY_ATTRIBUTES, *PSECURITY_ATTRIBUTES, *LPSECURITY_ATTRIBUTES;

typedef struct _SECURITY_DESCRIPTOR
{
    UCHAR Revision;
    UCHAR Sbz1;
    SECURITY_DESCRIPTOR_CONTROL Control;
    PSID Owner;
    PSID Group;
    PACL Sacl;
    PACL Dacl;
} SECURITY_DESCRIPTOR, *PSECURITY_DESCRIPTOR;
```

You should not try to work directly with the SECURITY_DESCRIPTOR structure; instead, use the API functions that enable you to read and write to a security descriptor. The API functions will continue to work even while the structure of the SECURITY_DESCRIPTOR changes. These functions include:

- `GetSecurityDescriptorDacl()`
- `GetSecurityDescriptorSacl()`
- `GetSecurityDescriptorGroup()`
- `GetSecurityDescriptorLength()`
- `GetSecurityDescriptorOwner()`
- `InitializeSecurityDescriptor()`
- `IsValidSecurityDescriptor()`
- `MakeAbsoluteSD()`
- `MakeSelfRelativeSD()`
- `SetSecurityDescriptorDacl()`
- `SetSecurityDescriptorSacl()`
- `SetSecurityDescriptorGroup()`
- `SetSecurityDescriptorOwner()`

Two types of security descriptors are used in NT:

- The absolute security descriptor has pointers to the ACL structures.
- The self-relative security descriptor is self-contained with embedded ACL.

The advantage of the self-relative security descriptor is that it can be transmitted electronically (because of its flat format) or saved to a file or the registry. Two functions enable you to convert between the two types of security descriptors: `MakeSelfRelativeSD()` and `MakeAbsoluteSD()`.

Chapter 8, “COM and the Registry,” showed how to save and load self-relative security descriptors in the registry. Another important task you must be able to perform is saving these self-relative security descriptors in files. Listing 12.2 shows how to do that.

### LISTING 12.2 Save a Security Descriptor in a File

```cpp
#include <windows.h>
#include <fstream.h>

// SaveSecurityDescriptorToFile
//
int SaveSecurityDescriptorToFile(PSECURITY_DESCRIPTOR pSD,
                                 ofstream & ofs)
{
    // convert the security descriptor to
    // self-relative security description
    PSECURITY_DESCRIPTOR pSRSD = NULL;
    DWORD cbSD = 0;
    if (!::MakeSelfRelativeSD(pSD, pSRSD, &cbSD))
    {
        DWORD dw = ::GetLastError();
        if (dw != ERROR_INSUFFICIENT_BUFFER )
        {
            if (dw != ERROR_BAD_DESCRIPTOR_FORMAT)
            {
                std::cout << "Error ::MakeSelfRelativeSD "
```
