the next line. We save this as GetProcesses.py and run the application and we see something similar to Fig. 6.2.

![](bbox=[0.118, 0.143, 0.879, 0.365])

# ## 6.2 Running GetProcesses.py to retrieve remote information.

Now that we can obtain about processes, let's take a look at how to start a process. There may be times when we want to launch a payload remotely, or trigger an additional exploit. For this example we'll look at how to launch a process and then verify that it is running.

```
import winrm
# Place Script Here
script = ""
Start-Process 'C:\Program Files\Explorer\explorer.exe' -argument "http://www.nuix.com/ctat" -Start-Sleep -s 2
Get-Process ieplore winrm.Session('<host><ip>', auth=('<username>','<password>'))
r = ses.run_ps(script)
print r.std_out, r.std_err
```

We use the Start-Process cmdlet to launch explorer.exe with one option, "http://www.nuix.com/ctat", the Nuix Cyber Threat Team homepage. Powershell launches Internet Explorer in the background on the page, and we will use the Start-Sleep cmdlet to cause the script to sleep for 2 seconds. This will give