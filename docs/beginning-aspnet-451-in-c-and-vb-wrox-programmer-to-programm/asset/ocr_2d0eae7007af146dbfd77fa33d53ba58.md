```
    applicationName="/"
    />
    </providers>
    </membership>
```

This provider configuration features a number of interesting attributes, which are described in the following table. The default values listed in the description column are applied when you don’t specify the associated attribute in the configuration file.

| ATTRIBUTE | DESCRIPTION |
|---|---|
| connectionStringName | Points to the name of the connection string for the application. |
| enablePasswordRetrieval | Determines whether users are able to retrieve their current password. This option cannot be set when passwordFormat is Hashed (see passwordFormat). Defaults to false. |
| enablePasswordReset | Determines whether a user is able to request a new password. Defaults to true. |
| requiresQuestionAndAnswer | Determines whether controls like CreateUserWizard and PasswordRecovery have the user enter a security question and answer. Defaults to true. |
| applicationName | Provides the unique name of the application. Defaults to a forward slash (/), but you can change it to support multiple websites using the same database with different accounts. |
| requiresUniqueEmail | Determines whether the system allows duplicate e-mail addresses for user accounts. When set to true, each user must provide a unique username and a unique e-mail address. Defaults to true. |
| passwordFormat | Determines the way passwords are stored in the database. It supports the following formats:
Clear — Passwords are stored as plaintext.
Encrypted — Passwords are encrypted in a reversible format that enables the system to retrieve the clear text representation of the password again.
Hashed — Passwords are encrypted with an irreversible, one-way algorithm. When the passwordFormat is Hashed, users cannot retrieve their original passwords anymore. They can only request a new, auto-generated password. Defaults to Hashed. |