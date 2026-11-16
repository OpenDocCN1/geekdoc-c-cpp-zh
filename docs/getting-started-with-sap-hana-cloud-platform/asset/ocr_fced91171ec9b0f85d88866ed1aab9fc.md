For general-purpose access to cloud-based database instances (including those based on SAP MaxDB), you can use the open-db-tunnel command of the Console Client to open a database tunnel on your local host. Listing 6.15 demonstrates the syntax required to run this command.

```
neo open-db-tunnel -h <host> -u <user> -a <account> --id <schema>
```

# Listing 6.15 Opening a Database Tunnel Using the Console Client

Once the tunnel is opened, the Console Client will display an output window like the one shown in Figure 6.19. Here, you are provided with JDBC connection details that can be used to establish connections in JDBC-based tools or stand-alone load or test programs written in Java. While this session is open, you can use the database tunnel to connect to the target database schema.

![](bbox=[0.15, 0.37, 0.78, 0.62])

# Figure 6.19 Creating a Database Tunnel Using the Console Client

To demonstrate how to utilize database tunnel connections for administrative purposes, let's take a look at how to set up a connection using the Eclipse Data Tools Platform (DTP). Here, the steps are as follows:

+   1. Open the DATA SOURCE EXPLORER view, as shown in Figure 6.20. This view is provided in conjunction with the Eclipse DTP and should be available by default in your Eclipse environment.

+   2. Within the DATA SOURCE EXPLORER view, create a new connection by right-clicking on the DATABASE CONNECTIONS node and choosing the NEW... menu option (Figure 6.21).