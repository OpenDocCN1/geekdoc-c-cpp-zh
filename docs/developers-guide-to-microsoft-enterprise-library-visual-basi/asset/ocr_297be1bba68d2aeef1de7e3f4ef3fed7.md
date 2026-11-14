```
Dim canUpdateSalesData As Boolean _
    = authProvider.Authorize("UpdateSalesData")
    Console.WriteLine("User can execute 'UpdateSalesData' task: {0}", _
    canUpdateSalesData)

    ' Determine whether user is authorized for rule defined as "ReadSalesData".
    Dim canReadSalesData As Boolean _
    = authProvider.Authorize("ReadSalesData")
    Console.WriteLine("User can execute 'ReadSalesData' task: {0}", _
    canReadSalesData)
End Sub
```

When you run this example, you will see output similar to that below. The code in the first example of this chapter, which authorizes the user and caches the identity and principal, defines the principal it generates as a member of only the FieldSalesStaff role, and so the user is authorized only for the ReadSalesData task.

```
The IPrincipal security token is '77a9c8Af-9691-4ae4-ab5-0e96d4c4610e'.
User can execute 'UpdateSalesData' task: False
User can execute 'ReadSalesData' task: True
```

# Using AzMan Provider Rules

The second example of authorization, Authorize a user for a process using AzMan rules, uses the Windows Authorization Manager (AzMan) provider. In the example, we defined rules for the same two tasks you saw in the previous example: UpdateSalesData and ReadSalesData. However, AzMan depends on being able to access Windows account details with the security identifier (SID), and so roles in the file named Example.xml we provide with the examples may not be able to authenticate you on your machine. It will only work if you are using a local machine account or your current domain logon account can access the Active Directory® store to obtain information. You should open the Example.xml file in AzMan (a snap-in for the Microsoft Management Console (MMC)) and edit the rules it contains to specify your own local or domain accounts to experiment with AzMan authorization.

The example code is similar to what you saw when we used the Security block authorization rule provider in the previous example. It obtains the current user principal from the security cache using the token stored in the application-level variable, and calls the same AuthorizeUserWithRules method as the previous example to check if this principal is authorized for the UpdateSalesData and ReadSalesData tasks. This example then generates a WindowsPrincipal for the current user and checks if this is authorized for the UpdateSalesData and ReadSalesData tasks.

The main differences in the code for this example are that it passes a reference to the AzMan authorization provider created when the program starts to the AuthorizeUser WithRules routine, as shown here.