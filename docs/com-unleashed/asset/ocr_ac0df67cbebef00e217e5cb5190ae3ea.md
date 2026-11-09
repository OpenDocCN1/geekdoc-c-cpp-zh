# **Listing 12.6** Continued

```
    BYTE SubAuthorityCount;
    SID_IDENTIFIER_AUTHORITY IdentifierAuthority;
    DWORD SubAuthority[ANYSIZE_ARRAY];
    } SID, *PSID;
```

Some SIDs are referred to as *well-known SIDs* because they represent well-known security principals. The following list shows these.

+   - Null SID: S-1-0-0
+   - World: S-1-1-0
+   - Local: S-1-2-0
+   - Creator Owner ID: S-1-3-0
+   - Creator Group ID: S-1-3-1
+   - Creator Owner Server ID: S-1-3-2
+   - Creator Group Server ID: S-1-3-3
+   - (Non-unique IDs): S-1-4
+   - NT Authority: S-1-5
+   - Dialup: S-1-5-1
+   - Network: S-1-5-2
+   - Batch: S-1-5-3
+   - Interactive: S-1-5-4
+   - Service: S-1-5-6
+   - AnonymousLogon: S-1-5-7
+   - Proxy: S-1-5-8
+   - ServerLogon: S-1-5-8
+   - (Logon IDs): S-1-5-5-X-Y
+   - (NT nonunique IDs): S-1-5-21-...
+   - (Built-in domain): S-1-5-32

A few API functions enable you to use, query, and modify SIDs. They are

+   - LookupAccountName()
+   - LookupAccountSid()
+   - IsValidSid()
+   - EqualSid()
+   - EqualPrefixSid()

![](bbox=[0.86, 0.36, 0.99, 0.6])