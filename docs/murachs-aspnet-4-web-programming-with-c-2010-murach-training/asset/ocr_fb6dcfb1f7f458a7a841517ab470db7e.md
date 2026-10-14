# The Provider tab of the Web Site Administration Tool

![](bbox=[0.155, 0.108, 0.839, 0.276])

# Elements in the web.config file that relax the default password policy

```
```xml
<membership defaultProvider="AspNetSqlMembershipProviderRelaxed">
    <providers>
        <add name="AspNetSqlMembershipProviderRelaxed"
             type="System.Web.Security.SqlMembershipProvider,
                   System.Web, Version=2.0.0.0, Culture=neutral,
                   PublicKeyToken=b03f5f7f11d50a3a"
             connectionStringName="LocalSqlServer"
             enablePasswordRetrieval="false"
             enablePasswordReset="true"
             requiresQuestionAndAnswer="true"
             applicationName="/"
             requiresUniqueEmail="false"
             passwordFormat="Hashed"
             maxInvalidPasswordAttempts="5"
             passwordAttemptWindow="10"
             passwordStrengthRegularExpression=""
             minRequiredPasswordLength="6"
             minRequiredNonalphanumericCharacters="0"/>
    </providers>
</membership>
```
```

# Description

+   - By default, a *data provider* named AspNetSqlProvider is used to store both membership and role data in a SQL Server Express database named AspNetDb.mdf. However, you can use separate membership and role providers, and you can write your own custom providers.
+   - The definitions for the default membership and role providers can be found in the machine.config file. This file is stored in the Config folder subordinate to the .NET Framework 4 installation folder.
+   - To relax the password restrictions for a provider, you can change the attributes for password length and non-alphanumeric characters in the web.config file for an application.

![](bbox=[0.125, 0.916, 0.859, 0.941])