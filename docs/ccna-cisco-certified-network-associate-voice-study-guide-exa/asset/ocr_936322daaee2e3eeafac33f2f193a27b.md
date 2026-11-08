If the Cisco router still detects the module but it is not working, the next step is to verify the proper configuration. To do this, you must first gain access to the service module. Access the service module with the following command:

```
```
Router1# service-module service-engine 1/0 session
CUE>
```
```

This command assumes that the Unity Express module is addressed as 1/0. If not, you'll simply change the command to match the address of your service module. Remember, this address can be identified by looking at the running-config. Notice that the prompt changes once you've accessed the service module. Once you've accessed the service module, you must again enter enable mode to perform any useful functions as follows:

```
```
CUE> enable
Password:
CUE#
```
```

Now you can begin verifying proper configuration. The Unity Express module requires that appropriate license files be installed. To verify the license, use the following command:

```
```
CUE# show software license
```
```

You should see results that indicate a license file is installed and the number of mailboxes the license supports.

In worst-case scenarios, you can reset the Unity Express module to factory defaults. If you take this drastic action, all configuration and data will be lost, so this action should be taken with caution. You will be warned by the device should you choose to perform this action. To reset to factory defaults, execute the following commands:

```
```
CUE> offline
CUE (offline)> restore factory default
```
```

After executing the offline command, you'll be asked to verify the action. Simply type Y and press ENTER. You'll also be asked to verify the second command. Type Y and press ENTER if you're absolutely certain you must take this last-resort action.