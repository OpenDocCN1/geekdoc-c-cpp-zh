# # Appendix E Encrypting Configuration Files

Enterprise Library supports encryption of configuration information. Unless your server is fully protected from both physical incursion and remote incursion over the network, you should consider encrypting any configuration files that contain sensitive information, such as database connection strings, passwords and user names, or validation rules.

You can select any of the encryption providers that are included in your system’s Machine.config file. Typically, these are the **DataProtectionConfigurationProvider**, which uses the Microsoft® Windows® Data Protection API (DPAPI), and the **RsaProtectedConfigurationProvider**, which uses RSA. The settings for these providers, such as where keys are stored, are also in the Machine.config file. You cannot edit this file with a configuration tool; instead, you must modify it using a text editor or an operating system configuration tool.

As an example of the effect of this option, the following is a simple unencrypted configuration for the Data Access block.

```
<dataConfiguration defaultDatabase="Connection String" />
<connectionStrings>
  <add name="Connection String"
    connectionString="Database=TheImportantOne; Server=WEHAVELIFTOFF;
    User ID=secret; Password=DontTellNE1"
    providerName="System.Data.SqlClient" />
</connectionStrings>
```

When you specify the **DataProtectionConfigurationProvider** option, the resulting configuration section looks like the following.

```
<dataConfiguration
  configProtectionProvider="DataProtectionConfigurationProvider">
  <EncryptedData>
    <CipherData>
      <CipherValue>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAAbCHTvqG8QbuQI1BYa0uH
yTm50vQjNdSiohA5Fo6bXQh0R5VsvUxdcFNuGkHuhUaH15RZSN5WDM2CDmiQg
...
JyEadytIBvTbCmxXefuWNSMT/ T
```