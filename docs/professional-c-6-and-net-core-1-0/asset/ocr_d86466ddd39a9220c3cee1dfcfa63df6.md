IGroupManager. This interface defines two methods: Add and Remove. Both of these methods need a group name and a connection identifier to add or remove the specified connection to the group. The connection identifier is a unique identifier associated with a client connection. The client connection identifier—as well as other information about the client—can be accessed with the Context property of the Hub class. The following code snippet invokes the Add method of the IGroupManager to register a group with the connection, and the Remove method to unregister a group (code file ChatServer/GroupChatHub.cs):

```
public Task AddGroup(string groupName) =>
    Groups.Add(Context.ConnectionId, groupName);

public Task LeaveGroup(string groupName) =>
    Groups.Remove(Context.ConnectionId, groupName);
```

> NOTE The Context property of the Hub class returns an object of type HubCallerContext. With this class, you can not only access the connection identifier associated with the connection, but you can access other information about the client, such as the header, query string, and cookie information from the HTTP request and also information about the user. This information can be used for user authentication.

Invoking the Send method—this time with three parameters including the group—sends information to all connections that are associated with the group. The Clients property is now used to invoke the Group method. The Group method accepts a group string to send the MessageToGroup message to all connections associated with the group name. With an overload of the Group method you can add connection IDs that should be excluded. Because the Hub implements the interface IGroupClient, the Groups method returns the IGroupClient. This way, the MessageToGroup method can be invoked using compile-time support (code file ChatServer/GroupChatHub.cs):

```
public void Send(string group, string name, string message)
{
    Clients.Group(group).MessageToGroup(group, name, message);
}
```

Several other extension methods are defined to send information to a list of client connections. You’ve seen the Group method to send messages to a group of connections that’s specified by a group name. With this method, you can exclude client connections. For example, the client who sent the message might not need to receive it. The Groups method accepts a list of group names where a message should be sent to. You’ve already seen the All property to send a message to all connected clients. Methods to exclude sending the message to the caller are OthersInGroup and OthersInGroups. These methods send a message to one specific group excluding the caller, or a message to a list of groups excluding the caller.