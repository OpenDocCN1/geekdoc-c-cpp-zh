![](bbox=[0.107, 0.139, 0.806, 0.563])

Figure 2.1  Setting system properties in Windows 10

behind the Windows Settings dialog. If you can’t find it anywhere, try running `sysdm.cpl` from the Run dialog that you get by holding down the Windows and R key at the same time, and then select the Advanced tab and click the Environment Variables button.) Locate and select a variable named Path in the User Variables list. Click the Edit button, then the New button, and add an entry with the `jdk\bin` directory (see Figure 2.2).

Save your settings. Any new “Command Prompt” windows that you start will have the correct path.

Here is how you test whether you did it right: Start a terminal window. Type the line

```
```text
javac --version
```
```

and press the Enter key. You should get a display such as this one:

```
```text
javac 11.0.1
```
```