
# Owner Rights

Because owners of an object can normally override the security of an object by always being granted read-control and write-DACL rights, a specialized method of controlling this behavior is exposed by Windows: the Owner Rights SID.

The Owner Rights SID exists for two reasons:

- To improve service hardening in the operating system Whenever a service creates an object at run time, the Owner SID associated with that object is the service running (in such local system or local service) and not the actual service SID. This means that any other service in the same account would have access to the object by being an owner. The Owner Rights SID prevents unwanted behavior.

- To allow more flexibility for specific usage scenarios For example, suppose an administrator wants to allow users to create files and folders but not modify the ACLs on them (Users can inadvertently or maliciously grant access to files or folders to unwanted accounts). By using an inheritable Owner SID, they can be prevented from editing or viewing the ACL on the objects they create. A second usage scenario relates to group changes. Suppose an employee has part of some confidential or sensitive group, has created several files while a member of that group, and has now been removed from the group for reasons. Because employee is still a user, he could continue accessing the sensitive files.

The second algorithm is used to determine whether a specific access request be granted based on the caller's access token. Each open function in the Windows API that deals with securable objects has a parameter that specifies the desired access mask, which is the last component of the security equation. To determine whether the caller has access, the following steps are performed:

- 1. If the object has no DACL (a null DACL), the object has no protection and the security system grants the desired access.

- 2. If the caller has the take-ownership privilege, the security system grants write-owner access if requested and examines the DACL. However, if write-owner access is the only access requested by a caller with take-ownership privilege, the security system grants that access and never examines the DACL.

- 3. If the caller is the owner of the object, the system looks for an OWNER_RIGHTS SID and uses that SID as the SID for the next steps. Otherwise, read-control and write-DACL access rights are granted. If these were the only access that the caller requests, access is granted without examining the DACL.

- 4. Each ACE in the DACL is examined from first to last. An ACE is processed if one of the following conditions is satisfied:

  - The ACE is an access-deny ACE, and the SID in the ACE matches an enabled SID (SIDs can be disabled) or a deny-only SID in the caller's access token.

  - The ACE is an access-allowed ACE, the SID in the ACE matches an enabled SID for the caller’s token that isn’t of type deny-only.

  - It is the second pass through the descriptor for restricted-SID checks, and the SID in the ACE matches a restricted SID in the caller’s access token.

  - The ACE isn't marked as inherit-only.

- 5. If it is an access-allowed ACE, the rights in the access mask in the ACE that were requested granted. If all the requested access rights have been granted, the access check succeeds. If it is an access-denied ACE and any of the requested access rights are in the denied-access rights, access is denied to the object.

- 6. If the end of the DACL is reached and some of the requested access rights haven’t been granted, access is denied.

- 7. If all accesses are granted the caller’s access token has at least one restricted SID, the system rescans the DACL’s ACEs locking for ACEs with access-mask masks for the users it is requesting and a match of the ACE’s SID with any of the caller’s restricted SIDs. If only both scans of the DACL granted requested access rights is the user granted access to the object.

The behavior of both access-validation algorithms depends on the relative ordering of allow and deny ACEs. Consider an object with two ACEs: one that specifies a certain user is full access to an object and one that denies the user. If the allow ACE precedes the deny ACE, the user can obtain full access to the object, but if the order is reversed, the user cannot gain any access to the object.

Several Windows functions, such as SetSecurityInfo and NamedSecurityInfo, apply ACEs in the preferred order of explicit deny ACEs preceding allow ACEs. For example, the security editor dialog boxes with which you edit permissions on NTFS files and registry keys use these functions. SetSecurityInfo and NamedSecurityInfo also apply inheritance rules to the security descriptor on which they are applied.

Figure 7-9 shows an example of access validation the importance of ACE ordering. In the example, access is denied to a user wanting to open a file even though an ACE in the object’s DACL grants the access. This is because the ACE denying the user access (by virtue of the user’s membership in the Writers group) precedes the ACE granting access.

# Access Token

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_679_0.png)

FIGURE 7-9 Access-validation example.

As stated, because it wouldn't be efficient for the security system to process the DACL every time a process uses a handle, the SRM makes this check only when a handle is opened, not each time the handle is used. Thus, once a process successfully opens a handle, the security system can't revoke the access rights that have been granted, even if the object's DACL changes. Also keep in mind that kernel-mode code uses pointers rather than handles to objects, the access check isn't performed when operating system objects. In other words, the Windows executes itself (and all loaded drivers) in a security sense.

The fact that an object's owner is always write-DACL access to an object means that users can never be prevented from accessing the objects they own. If, for some reason, an object had an empty DACL (no access), the owner would still be able to open the object with write-DACL access and then apply a new DACL with the desired permissions.

# A warning regarding the GUI security editors

When you use the GUI permissions to modify security settings on a file, a registry, or an Active Directory object, the main security dialog box shows a potentially misleading view of the security that's applied to the object. If you allow Full Control to the Everyone group and deny the Administrator Full Control, the list might lead you to believe that the Everyone group access-allowed ACE permits the Administrator ACE because that's the order in which they appear. However, as we've said, the editors place deny ACEs before allow ACEs when they apply the ACL to the object.

The Permissions tab of Advanced Security Settings shows the ACEs in the DACL. However, even this dialog box can be confusing because a complex DACL can have deny ACEs for various accesses followed by allow ACEs for other types.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_680_0.png)

# Advanced Security Settings for Dummy.txt

| Name | G:\Temp\Dummy.txt | |
| --- | --- | --- |
| Owner | Pavel Yovich (radiacon@live.com) | Change |
| Permissions | Auditing | Effective Access |

| Type | Principal | Access | Inherited from |
| --- | --- | --- | --- |
| Deny | Administrators | Full control | None |
| Allow | Everyone | Full control | None |
| Allow | Authenticated Users | Modify | None |
| Allow | SYSTEM | Full control | None |
| Allow | Users | Read & execute | None |

The only definitive way to know what access a particular user or group will have an object (other than that user or a member of the group try to access the object) is to use the Effective Access tab of the dialog box that is displayed when you click the Advanced button in the Properties dialog box. Enter the name of the user or group you want to check and the dialog box shows you which permissions they are allowed for the object.

Effective Access allows you to view the effective permissions for a user, group, or account. If the account is a member of a group you can see the impact of potential additions to security tokens for the account. When you evaluate the impact of adding a group, any group that the intended group is member of must be added separately.

/Group: Pavel Yovich (radiacon@live.com) Select a user

| Effective access | Permissions | Access limited by |
| --- | --- | --- |
| X | Full control | File Permissions |
| X | Traverse folder / execute file | File Permissions |
| X | List folder / read data | File Permissions |
| X | Read attributes | File Permissions |
| X | Read extended attributes | File Permissions |
| X | Create files / write data | File Permissions |
| X | Create folders / append data | File Permissions |
| X | Write attributes | File Permissions |
| X | Write extended attributes | File Permissions |
| | Delete | |
| Read permissions | | |
| Change permissions | | |
| X | Take ownership | File Permissions |
