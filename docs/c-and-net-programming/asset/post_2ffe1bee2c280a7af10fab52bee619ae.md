
- Double-clicking (or tapping) on any service will open its properties, which is where the purpose for the service can be seen and, for some services, what will happen if it is stopped. For example, opening the properties for **Apple Mobile Device Service** explains that the service is used to communicate with **Apple device** that is plugged into the computer.
- The properties of a service cannot be viewed if accessed through Task Manager. The Services utility is to be used to see the properties.
- In the Services window, for each of the services listed, five things can be found namely,
  1. Name - The name of the service can be helpful to get an idea of what that service does. Unfortunately, though, this name is often too cryptic to help to understand what the service is all about.
  2. Description - The description of the service shows some brief information about the service's purpose or identity.
  3. Status - Indicates whether that service is running or if it is stopped.
  4. Startup Type - Shows how that service is started by Windows. Services can be launched automatically, automatically but with a delay, manually, or they can be disabled, which means that they are never started.
  5. Log On As - It allows you to select whether the service is started using the Local System account or using another user account that is manually specified.
- It should be noted that the same information can be viewed in the Properties of each service, by double-clicking (or double-tapping) on its name in the Services window.

## 25.1.3 Types of Windows Services

Windows Services broadly fall into three categories depending on the actions and applications they control: Local Services, Network Services and System. Third party applications such as antivirus software may also install their own services.

## 25.1.4 Accessing and Managing Windows Services

- There are quite a few different ways of accessing the Windows services. A simple technique is to use the search option in Windows. Enter the word services in the search field from the taskbar in Windows 10, start typing services on the Start screen from Windows 8.1, or type services in the search field from the Start Menu in Windows 7. In all these operating systems, click or tap on the Services or "View local services" search results. Then, the Services window opens. The Services window is the place from which one can view, start, stop and configure any Windows service.

- Windows Services are managed via the **Services Control Manager panel**. The panel shows a list of services and for each, name, description, status (running, stopped or paused) and the type of service. Double-clicking on a service reveals its properties in greater detail. One can stop, pause, start, delay start, or resume each service as appropriate. One can also modify the start mechanism (Manual or Automatic) or specify an account.
- Services can be deleted by a user with administrative privileges, but as doing so can render the operating system unstable, it should be done only when necessary and with caution.

### 25.1.4.1 The Services Panel

- Windows has always used the Services panel as a way to manage the services that are running on the computer. One can get there at any point by hitting WIN + R on the keyboard to open the Run dialog, and typing in services.msc.
- The Services panel is fairly simple: there are a list of services, a status column to show whether it is running or not, and more information like name, description, and the startup type of the service. It can be noticed that not every service is running all the time.
- While one can select a service and either right-click it or click the toolbar buttons to start, stop, or restart it, one can also double-click to open up the properties view and get more information.
- Disabling the service is as simple as changing the Startup type drop-down to disabled and choosing Apply, although one can also change it to Manual or automatic with a delayed start. From this dialog one can see the full path to the executable as well, which can help in many cases when one wants to see what exactly the service is running.
- The **Log On tab** allows you to choose whether the service is logged on as the local system account or under another account. This is mostly useful in a server environment where one might want to run a service account from the domain that has access to resources on other servers.
- One might notice the option for "Allow service to interact with desktop", that is - by default, services are not allowed to access the desktop unless this box is checked, and this checkbox is really only there for legacy support.
- But just checking that box doesn't immediately give them access - one would also need to make sure that the **NoInteractiveServices** value in the registry is set to 0, because when it is set to 1, that checkbox is ignored and services can't interact with the desktop at all. **In Windows 8, the value is set to 1, and interactive services are prohibited.**
- Services aren't supposed to be interactive because all windows exist in the same user terminal with access to common resources like the clipboard, and if they are running along with other processes there could be an issue where a malicious application running in a normal user process could attempt to gain more access through a service, and considering that services run as the local system account, that probably isn't a good thing.
- The Recovery tab allows you to choose options for what happens when the service fails. One can choose to automatically restart the service, which is generally the default option, or can run a program or restart the computer.
- Run a program option is probably the most useful, since one could set Windows to automatically send out an email if the service fails more than once - a helpful option in a server environment. It's definitely much less helpful on a regular desktop.
- The dependencies tab shows which services depend on a particular service, and which services depend on the one being viewed by the user.

### 25.1.4.2 More Information on Windows Services

- Services are different than regular programs in that a regular piece of software will stop working if the user logs out of the computer. A service, however, is running with the Windows OS, sort of in its own environment, which means the user can be logged completely out of their account but still have certain services running in the background.
- Though it may come off as a disadvantage to always have services running, it's actually very beneficial, like if **remote access software** is being used. An always-on service installed by a program like **TeamViewer** enables user to remote into computer even if user is not logged on locally.
- There are other options within each service's properties window on top of what is described above that allow you to customize how the service should start up (automatically, manually, delayed, or disabled) and what should automatically happen if the service suddenly fails and stops running.
- A service can also be configured to run under the permissions of a particular user. This is beneficial in a scenario where a specific application needs to be used but the logged in user doesn't have proper rights to run it.

### 25.1.4.3 Looking at Services in Task Manager for Windows 8.x

- The regular services panel hasn't changed much in years, but thankfully there is a much better way to look at which services are running, and which of those services are using a lot of resources.
- Task manager in Windows 8 has a new Services tab, which allows to stop and start services, but also comes with a "Search online" option, and even more useful, the "Go to details" option.
- Once Go to details option is selected from the menu, it is switched over to the Details tab, and the process that is responsible for that service will be highlighted.
- Right-click it again, and then select Go to Services. Now many services are selected in the Services window, and it can be noticed that they are all in the LocalSystemNetworkRestricted group and they are all currently running.

### 25.1.4.4 Using Process Explorer to Look at Services

To get a much clearer view of what services are running under each process, Process Explorer can be used that can find the service in the list, double-click it, and then go to the Services tab. This method works on any version of Windows. In Process Explorer all the services should be in the tree underneath services.exe.

### 25.1.4.5 Administering Services from the Command Prompt

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
sc stop TrkWks
```

To start it again below command can be used,

```
sc start <servicename>
```
