```
</authentication>
<authorization>
    <deny users="?" />
</authorization>
<membership defaultProvider="SqlProvider" userIsOnlineTimeWindow="15">
    <providers>
        <add
            name="SqlProvider"
            type="System.Web.Security.SqlMembershipProvider"
            connectionStringName="SqlServices"
            applicationName="MyApplication"
            enablePasswordRetrieval="false"
            enablePasswordReset="true"
            requiresQuestionAndAnswer="true"
            requiresUniqueEmail="false"
            passwordFormat="Hashed"
            maxInvalidPasswordAttempts="5"
            passwordAttemptWindow="10" />
    </providers>
</membership>
</system.web>
</configuration>
```

# The Membership Class

The Membership class allows you to create users for an ASP.NET application and manage these users. The users created for an ASP.NET application using the Membership class can access the ASP.NET application as authenticated users. The hierarchy of the Membership class is as follows:

System.Object
System.Web.Security.Membership

Table 36.21 lists the noteworthy methods of the Membership class:

| Table 36.21: Noteworthy Methods of the Membership Class |
| Method | Description |
| CreateUser() | Creates a new user for an ASP.NET application. |
| DeleteUser() | Deletes user of a specific user name. This method returns true if it deletes the user successfully and false if the user name of the user that is to be deleted does not exist. |
| FindUsersByEmail() | Returns those e-mail addresses that matches with any part of the e-mail address passed to the method. |
| FindUsersByName() | Returns the users, the user name of which matches with any part of the user name passed to the method. |
| GeneratePassword() | Provides a password of specific length. The password returned by the GeneratePassword() method contains specified number of non-alphanumeric characters. |
| GetAllUsers() | Returns users on the basis of the page index and page size passed to the method. |
| GetNumberOfUsersOnline() | Determines how many users are connected to the Internet currently. You cannot use this method if your application is using ActiveDirectoryMembershipProvider. |
| GetUserNameByEmail() | Returns the name of the user, the e-mail address of which is passed to the method. |
| UpdateUser() | Updates information of a user. |
| ValidateUser() | Verifies the credentials of a user. This method returns true if the credentials of the user are valid, otherwise false. |