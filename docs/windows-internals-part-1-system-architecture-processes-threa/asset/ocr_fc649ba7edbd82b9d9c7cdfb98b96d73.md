System32 and most of its subdirectories, %SystemRoot%Home, and a small number of directories under %ProgramFiles% (for example, containing Windows Defender and Windows Journals).

There are additional requirements, depending on the type of executable. EXE files other than Mmc.exe auto-elevate if they are requested via an auto-elevate element in their manifest. The manifest shown earlier of eventntr.exe in the previous section illustrates this.

Finally, COM (out-of-process server) can request administrative rights within their registry key. To do so requires a subnet named Elevation with a DWORD value named Enabled, Both the COM class and its instantiating executable must meet the Windows executable requirements, although the executable not have requested auto-elevation.

# Controlling UAC behavior

UAC can be modified via the dialog box shown in Figure 7-29. This dialog box is available under User Account Control Settings.

![](bbox=[0.166, 0.513, 0.589, 0.773])

FIGURE 7-29 User Account Control Settings dialog box.

The four possible settings have the effects described in Table 7-18.

The third position is not recommended because the UAC elevation prompt appears not on the Secure Desktop but on the normal user's desktop. This could allow a malicious program running in the same session to change the appearance of the prompt. It is intended for use in systems where the video subsystem takes a long time to dim the desktop or is otherwise unsuitable for the usual UAC display.