send a lot of feedback to the event log in order to make debugging easier. This is not advisable. Only important information should be logged in the event log. The next few sections show you a few tricks you can use to debug services.

# Debugging Your Services

There are several reasons why services are more difficult to debug than other processes. The first reason is that services do not have a desktop like other processes. Another reason is that services usually run using a special user account called the system account.

# The System Account

The system account has special privileges that grant the account access to the file system and many other security resources. But the system account is quite limited and does not have access to any network resources. It is a null session account, and null session accounts do not have access to network resources, even if everyone was granted access to a network resource.

Finally, you cannot log on to a machine by using the system account. This makes it very difficult to debug bugs that are related to the fact that the service is running under an account with a set of access rights different from the rights of an interactive user.

# Task Manager: Debug

You can debug a process, even a process running under the system account, by starting the debugging from Task Manager. From the Task Manager’s Processes tab, you can right-click on a process to get its context menu. From the context menu, select Debug, which launches your registered debugger and attaches the current running process. You can also start Developer Studio with the switch /P followed by the process ID of the running service that you want to debug.

# Start the Debugger with the AT Command

Another option for debugging is to acquire a command shell that runs in the security context of the system account. From the Start menu, select Run. Type the command at `9:05 /interactive cmd.exe`, where 9:05 is one minute into the future—that is, if the current time were 10:06, you would type `at 10:07 /interactive cmd.exe`. When the clock reaches 10:07, the scheduler will launch a command shell. Because the scheduler runs with the security context of the system account, so will the command shell. From this command shell, you can start Developer Studio or any other process, and that process will also run in the security context of the system account.