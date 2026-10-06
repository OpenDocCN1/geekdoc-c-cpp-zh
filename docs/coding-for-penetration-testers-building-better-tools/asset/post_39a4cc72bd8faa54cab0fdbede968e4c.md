
# Getting In

In order to put any of our PowerShell goodness to use, we first need to find a way onto the system. Depending on exactly what we want to do when we are on the machine, we may also need administrative access. There are a number of tasks that we can carry out just using the permissions of a standard user account, such as ping sweeping or port scanning, as these only require the normal level of access that any account has. In order to change settings or carry any actions on the system that we will likely need the same access from PowerShell.

In this chapter we're going to look at how to interact with PowerShell over the Windows Remote Management interface, WinRM. We will be able to set up WinRM on our test system, but many enterprise systems will already have installed. Once it is set up, we will look at how to interact with it from Kali.

# Setting Up a Windows 10 System

Before we can compromise our system with PowerShell, we first need to take our standalone Windows 10 workstation and enable remote administration. To do this, we will need to enable WinRM, the Windows Remote Management interface.

```
winrm quickconfig
rm set winrm/config/service/auth '@{Basic="true"'
rm set winrm/config/client/auth '@{Basic="true"'
rm set winrm/config/service '@{AllowUnencrypted="true"'
-Item WSMAN:\localhost\TrustedHosts -value ""
```

These commands will configure WinRM and then it will set some overrides that normally would not have to be in place. These commands will let us interact with WinRM as if we were part of a trusted host in the domain. Typically, if we were going to interact with one of these services we would be allowed to use Kerberos authentication as part of the domain, but as we have no domain, we have to cheat a bit.

Now we need to set up our Kali image to be able to interact with WinRM. We are going to use a Python module called “pywinrm.” To install it, we issue the command "pip install pywinrm" in Kali, and we will go out and fetch the requirements.

Next we want to build a sample script to verify that we can connect. We want to be able to verify that we were able to both connect and execute a PowerShell script.

```python
#!/usr/bin/python
import winrm
# Place Script Here
script = "whoami"
ses = winrm.Session('<host IP>', auth=('<username>,<password>'))
r = ses.run_ps(script)
print r.std_out
print r.std_err
```

This script begins with importing the winrm command so that we can interact with our remote Windows 10 system. We then create our script which just has the command "whoami" to print out who we are authenticated as. Finally we create a new session with the Session command. That session is then used to run our script and the return information is stored in our return variable, "r." This return variable has three pieces of information about the command that was run: the status_code, the std_out output, and the std_err error output. We print the output of both std_out and any errors that occurred. We save the script as "connect.py" and when we run it, we should see output similar to Fig. 6.1.

File Edit View Search Terminal Help

```
root@kali:~# python connect.py
desktop-900e28h1\sussurro

root@kali:~# 
```

# FIGURE 6.1 Running connect.py.

While this is just one way to get in, there are tons of different ways to gain access to a remote host. We will continue using the WinRM service throughout this chapter, but we will also focus on some additional ways to interact with PowerShell on a remote system.

# Note

For those looking for additional information regarding how we can make our entry to the system on which we would like to use our PowerShell scripts, or the tools written in any of the other languages discussed in this book, for that matter, there are a number of great texts out on the topic. A few of the better known:

- *Counter Hack Reloaded: A Step-by-Step Guide to Computer Attacks and Effective Defenses, 2nd Edition (ISBN: 978-0-13-148104-6), by Ed Skoudsis
- *Gray Hat Hacking: The Ethical Hackers Handbook, 4th Edition (ISBN: 978-0178323880), by Daniel Regalado, Shon Harris, Allen Harper, Chris Eagle, Jonathan Ness, Branko Spasojevic, Ryan Linn, and Stephen Sims
- *Hacking Exposed™ 7: Network Security Secrets & Solutions (ISBN: 978-0071780285), by Start McClure, Joel Scambray, and George Kurtz

# Penetration Testing Uses for PowerShell

We can use PowerShell in many ways during a penetration test. Since PowerShell has access to Microsoft’s .NET libraries as well as core operating system functions, there isn't much that we can't do with PowerShell. We will go over a few uses for PowerShell, such as controlling processes and services, interfacing with the event logs, sending and receiving files over the network, and interfacing with the Registry.

# Controlling Processes and Services

Being able to create and destroy process and interact with services is one of the key capabilities required on a pen test. There are frequently times when we will have to run commands to gain additional insight into systems or to further our access. For this section, we will continue to focus on our WinRM scripts, but the PowerShell that we are running can be used directly from PowerShell on the remote system as well. Let's start with an example of getting a remote process list.

```python
import winrm
# Place Script Here
script = """Get-WmiObject Win32_Process|select ProcessId, ProcessName, CommandLine | Sort-Object ProcessId"""
ses = winrm.Session('<username>','<password>',auth='Basic')
r = ses.run_ps(script)
print r.std_out , r.std_err
```

In our example we use the Get-WmiObject cmdlet to retrieve the process table from the system. There is a lot of information returned about running processes by this cmdlet, but we only care about a subset. The Select cmdlet allow us to choose only certain fields to be displayed. We limit it to just the ProcessId, ProcessName, and CommandLine fields. Finally, we want to sort these processes by ProcessId, so we use the Sort-Object cmdlet to sort the output by the ProcessId. We will notice that our command spans two lines in our file, and the `` ` character says that the command is continued on the next line.

## 6.2 Running GetProcesses.py

Now that we have a process to work with, we can set about it. In PowerShell, we can kill a process using the Stop-Process cmdlet. In order to get the list of services, we can run Get-Service and the service name will get us the information for a specific service. We can also query the WMI object similar to how we did with processes.

```python
import winrm
# Place Script Here
script = "Get-WmiObject Win32_Service | Where-Object ($_.State -eq 'Running') | Select Name, Status"
```

Here we use the Get-WmiObject cmdlet to get the services table.
