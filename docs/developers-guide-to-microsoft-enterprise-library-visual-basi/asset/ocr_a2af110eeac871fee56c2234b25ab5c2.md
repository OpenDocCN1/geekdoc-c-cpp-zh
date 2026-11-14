For more information about configuring the Caching block, see Chapter 5, “A Cache Advance for your Applications.” For more information about configuring the Cryptography block, see Chapter 7 “Relying Cryptography Complexity.”

# CONFIGURING AUTHORIZATION RULES

The way that you configure your authorization rules depends on the type of authorization provider you are using. If you use the AzMan provider, you must configure the authorization rules using the AzMan GUI, or through the command line or scripting. If you choose to use the standard authorization rule provider instead, you must configure the authorization rules for this provider.

Each rule equates to a task or operation that your users may perform, and for which you want to be able to authorize these users to check if they should be allowed to execute “… that task.” Click the “…” button in the Rule Expression property of an Authentication Rule to open the Rule Expression Editor dialog, which makes it easier to generate the expressions for each of the rules you define. It helps you to insert the appropriate tokens that indicate individual identities, roles, and anonymous users; plus the operators that allow you to specify compound rules. For example, the following expression identifies users who are members of the Managers role or have the names Alice or Bob, but excludes any managers who are also members of the ITAdmin role:

```
(R:Managers OR I:Alice OR I:Bob) AND NOT R:ITAdmin
```

If you specify this expression for a rule named Update Database, you can use the Authorize method of the Security block to ensure that only users for whom the expression evaluates to true can execute this task. You’ll see how in the following sections of this chapter.

# How Do I Use the Security Block?

After you configure the block, as described in the previous sections of this chapter, you can write code in your application that uses the features of the block. However, first you must add references to the appropriate Enterprise Library assemblies to your project. In addition to the Enterprise Library assemblies you require in every Enterprise Library project (listed in Chapter 1, “Introduction”), you should reference or add to your bin folder the following assemblies:

+   - Microsoft.Practices.EnterpriseLibrary.Security.dll
+   - Microsoft.Practices.EnterpriseLibrary.Security.Cryptography.dll
+   - Microsoft.Practices.EnterpriseLibrary.Security.Cache.CachingStore.dll
+   - Microsoft.Practices.EnterpriseLibrary.Security.Caching.dll
+   - Microsoft.Practices.EnterpriseLibrary.Security.Caching.Cryptography.dll
+   - Microsoft.Practices.EnterpriseLibrary.Security.AzMan.dll

You need the caching assemblies only if you are using a cache to store credentials. You need the AzMan assembly only if you are using the AzMan rule store.