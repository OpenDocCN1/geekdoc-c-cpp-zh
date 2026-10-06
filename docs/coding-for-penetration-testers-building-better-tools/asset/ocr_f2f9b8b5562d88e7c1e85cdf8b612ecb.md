the event logs is to look at what we have on the system. For this, we can use the Get-EventLog cmdlet, with the list argument, as in Get-EventLog -List. When we run this cmdlet, we should see output similar to that shown in Fig. 6.5.

![](bbox=[0.118, 0.196, 0.865, 0.405])

# Fig 6.5 Output from getEvents.py.

Convenient, once we have the list of event logs in hand, we can use the same cmdlet with a different argument to list the content of a specific log. When we look at a log on a given system, there will likely be a very large amount of information in it, so will also want to filter what is returned to us, unless we are jumping the log contents out to a file. We can get the last few messages from the log that we specify by using the -newest argument with Get-EventLog, as import winrm

```
# Place Script Here
script = ""
Get-EventLog -List | ForEach-Object { Get-EventLog $_.Log -Newest 10 }

s = winrm.Session('172.16.85.130', auth=
('sussurro','Abc123!'))
r = ses.run_ps(script)
print r.std_out
```