To obtain the SID of a domain account, enter the user name with the domain as a prefix:

```
c:\>psgetsid redmon\johndoe
```

You can determine the SID of a domain by specifying the domain's name as the argument to PsGetSid:

```
c:\>psgetsid Redmon
```

Finally, by examining the RID of your own account, you know at least a number of security accounts (equal to the number resulting from subtracting 999 from your RID) have been created in your domain or your local machine (depending on whether you are using a domain or local machine account). You can determine what accounts have been assigned RIDs by passing a SID with the RID you want to query to PsGetSid. If PsGetSid reports that no mapping between the SID and account name was possible and the RID is lower than that of your account, you know that the account has been deleted.

For example, to find the name of the account assigned the 28th RID, pass the domain appended with -1027 to PsGetSid:

```
c:\>psgetsid S-1-5-21-1787744166-3910675280-2727264193-1027
```

Account for S-1-5-21-1787744166-3910675280-2727264193-1027:
User: johndoe

Process Explorer can also show you account and group SIDs through its Security tab. This tab shows information as who owns this process and groups the account is a member of. To view this information, double-click any process (for example, Process.exe) in the List and then click the Security tab. You would see similar to the following:

![](bbox=[0.19, 0.577, 0.89, 0.863])