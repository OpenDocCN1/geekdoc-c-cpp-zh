You can retrieve information about the user's computer, operating system, and amount of memory with My.Computer.Info (Figure 1.10).

If you want to know the name of the user, you can use

```
UserNameString = My.User.Name
```

In the following section, you will use My.Application to retrieve the assembly information about an application.

# Figure 1.10

Use My.Computer.Info to retrieve information about the user's computer.

![](bbox=[0.27, 0.32, 0.58, 0.52])

# Using Assembly Information

You can set an application's assembly information, also called the assembly attributes, and retrieve the information at run time.

# Setting the Assembly Information

You can view and set an application's assembly information in the Assembly Information dialog box. Double-click on My Project in the Solution Explorer to display the Project Designer's Application tab (refer to Figure 1.8); then click on the Assembly Information button, which displays the dialog box. Figure 1.11 shows the default information for an application called WindowsApplication1.

> TIP
> Always give the new project a name when you create it, which sets the root namespace, assembly name, and project name.

# Figure 1.11

The Assembly Information dialog box with the values supplied by default. You can edit the entries to the values of your choice.

![](bbox=[0.22, 0.81, 0.55, 0.97])