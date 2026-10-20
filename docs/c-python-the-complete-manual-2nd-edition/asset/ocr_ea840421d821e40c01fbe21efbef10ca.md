# # OS Module

The OS module allows you to interact directly with the built-in commands found in your operating system. Commands vary depending on the OS you're running, as some will work with Windows whereas others will work with Linux and macOS.



One of the primary features of the OS module is the ability to list, move, create, delete and otherwise interact with files stored on the system, making it the perfect module for backup code.



```
```python
import os
home=os.getcwd()
print(home)
```
```

![](bbox=[0.05, 0.75, 0.45, 0.92])



The returned result from printing the variable home is the current user's home folder on the system. In our example that's '/home/pi', it will be different depending on the user name you log in as and the operating system you use. For example, Windows 10 will output: C:\Program Files (x86)\Python36-32



![](bbox=[0.52, 0.4, 0.95, 0.55])



Yet another interesting element to the OS module, is its ability to launch programs that are installed in the host system. For instance, if you wanted to launch the Chromium browser from within a Python program you can use the command:

```
```python
import os
browser=os.system("/usr/bin/chromium-browser")
```
```

![](bbox=[0.52, 0.9, 0.95, 0.98])