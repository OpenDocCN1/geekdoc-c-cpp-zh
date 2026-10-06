install it, we issue the command "pip install pywinrm" in Kali, and we will go out and fetch the requirements.

Next we want to build a sample script to verify that we can connect. We want to be able to verify that we were able to both connect and execute a PowerShell script.

```
#!/usr/bin/python
import winrm
# Place Script Here
script = ""
whoami
"""
ses = winrm.Session(<host IP>', auth=('<username>,<password>'))
r = ses.run_ps(script)
print r.std_out
print r.std_err
```

This script begins with importing the winrm command so that we can interact with our remote Windows 10 system. We then create our script which just has the command "whoami" to print out who we are authenticated as. Finally we create a new session with the Session command. That session is then used to run our script and the return information is stored in our return variable, "r." This return variable has three pieces of information about the command that was run: the status_code, the std_out output, and the std_err error output. We print the output of both std_out and any errors that occurred. We save the script as "connect.py" and when we run it, we should see output similar to Fig. 6.1.