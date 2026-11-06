# OS Module

The OS module allows you to interact directly with the built-in commands found in your operating system. Commands vary depending on the OS you’re running, as some will work with Windows whereas others will work with Linux and macOS.

# INTO THE SYSTEM

One of the primary features of the OS module is the ability to list, move, create, delete and otherwise interact with files stored on the system, making it the perfect module for backup code.

+   **STEP 1** — You can start the OS module with some simple functions to see how it interacts with the operating system environment that Python is running on. If you’re using Linux or the Raspberry Pi, try this:

```
```python
import os
home=os.getcwd()
print(home)
```
```

![](bbox=[0.066, 0.462, 0.491, 0.637])

+   **STEP 2** — The returned result from printing the variable home is the current user’s home folder on the system. In our example that’s `/home/pi`; it will be different depending on the user name you log in as and the operating system you use. For example, Windows 10 will output: `C:\Program Files (x86)\Python36-32`.

![](bbox=[0.066, 0.741, 0.491, 0.921])

+   **STEP 3** — The Windows output is different as that’s the current working directory of Python, as determined by the system; as you might suspect, the `os.getcwd()` function is asking Python to retrieve the Current Working Directory. Linux users will see something along the same lines as the Raspberry Pi, as will macOS users.

![](bbox=[0.509, 0.441, 0.934, 0.637])

+   **STEP 4** — Yet another interesting element to the OS module, is its ability to launch programs that are installed in the host system. For instance, if you wanted to launch the Chromium browser from within a Python program you can use the command:

```
```python
import os
browser=os.system(“/usr/bin/chromium-browser”)
```
```

![](bbox=[0.509, 0.756, 0.934, 0.921])