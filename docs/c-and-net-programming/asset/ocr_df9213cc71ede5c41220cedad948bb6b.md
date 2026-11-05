# 25.1.4.3 Looking at Services in Task Manager for Windows 8.x

+   - The regular services panel hasn't changed much in years, but thankfully there is a much better way to look at which services are running, and which of those services are using a lot of resources.
+   - Task manager in Windows 8 has a new Services tab, which allows to stop and start services, but also comes with a "Search online" option, and even more useful, the "Go to details" option.
+   - Once Go to details option is selected from the menu, it is switched over to the Details tab, and the process that is responsible for that service will be highlighted.
+   - Right-click it again, and then select Go to Services. Now many services are selected in the Services window, and it can be noticed that they are all in the LocalSystemNetworkRestricted group and they are all currently running.

# 25.1.4.4 Using Process Explorer to Look at Services

To get a much clearer view of what services are running under each process, Process Explorer can be used that can find the service in the list, double-click it, and then go to the Services tab. This method works on any version of Windows. In Process Explorer all the services should be in the tree underneath services.exe.

# 25.1.4.5 Administering Services from the Command Prompt

Some operations just can't be done through the graphical user interface. To delete a service, for example, the command line can be used. The status of a service can be queried using the sc command, like,

```
sc qc eventlog
```

There are many other commands and operations that can be performed, including deleting a service, which is recommended if there are malwares on the system that is running as a service.

```
sc delete <malwareservicename>
```

Other operations can be done through command line, like stopping and restarting services from using the sc utility. For example, to stop the distributed link tracking client, below command can be used,

```
sc stop TrikWks
```

To start it again below command can be used,

```
sc start <servicename>
```