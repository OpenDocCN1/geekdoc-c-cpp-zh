```
secCache.ExpirePrincipal(principalToken)
Console.WriteLine("The principal for this token has been expired " _
    & "and removed from the cache.")
Else
    Console.WriteLine("You do not have a token that you can use to " _
        & "expire an identity.")
End If
```

When you run this example, you will see the values of the tokens before they are expired, and messages indicating that they were removed from the cache.

```
The IIdentity security token is 'e303fd67-331a-45b8-94d4-088746e2cacd'.
The identity for this token has been expired and removed from the cache.

The IPrincipal security token is 'd6563752-78ed-489a-86fa-efd76c979a76'.
The principal for this token has been expired and removed from the cache.
```

# CHECKING IF A USER IS AUTHORIZED TO PERFORM A TASK

One of the main reasons for using the Security block to manage identities is that it makes it easy to check if a user is authorized to perform a specified task or operation. The Security block contains two authorization providers, though you can create your own and integrate them with the Security block if you wish.

To check if a user is authorized, you call the Authorize method of an authorization provider, passing to it the user principal and the name of the task or operation. The Authorize method returns either True or False. The two providers included in the block are the authorization rule provider and the AzMan authorization provider (for details of these providers, see “What Are Authorization Rule Providers?” near the beginning of this chapter). The examples we present for this chapter include one that uses the authorization rule provider and one that uses the AzMan authorization provider.

# Using Security Block Configured Rules

If you only need to store authorization rules within the configuration of your application and have them fully managed by the Security block, you can use the authorization rule provider. As you saw earlier in this chapter, you configure a series of authorization rules for your application. Each rule defines an expression that specifies which users can access a specific task or carry out a specific operation.

The example Authorize a user for a process using a stored rule demonstrates this approach to authorization. In the application configuration we defined two rules:

+   * The rule named UpdateSalesData uses the expression “R:Administrators OR R:SalesManagers.” This allows a user who is a member of the Administrators role or the SalesManagers role to execute this task.

+   * the rule named ReadSalesData uses the expression “R:Users OR R:FieldSalesStaff OR R:SalesManagers.” This allows a user who is a member of the Users, FieldSalesStaff, or SalesManagers role to execute this task.