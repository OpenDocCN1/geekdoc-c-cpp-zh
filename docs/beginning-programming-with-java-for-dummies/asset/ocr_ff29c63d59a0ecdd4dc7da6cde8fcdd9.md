5. If your preferred version of Java appears in the Installed JREs list, put a check mark in that version's check box.

6. If your preferred version of Java doesn't appear in the Installed JREs list, click the Add button.

When you click the Add button, a JRE Type dialog appears (see Figure 2-14).

![](bbox=[0.22, 0.275, 0.6, 0.515])

Figure 2-14:
The JRE Type dialog.

7. In the JRE Type dialog, double-click Standard VM.

As a result, a JRE Definition dialog appears (see Figure 2-15). What you do next depends on a few different things.

8. Fill in the dialog's JRE Home field.

How you do this depends on your operating system.

+   - On Windows, browse to the directory in which you've installed your preferred Java version. On my many Windows computers, that directory is either `C:\Program Files\Java\jre8`, `C:\Program Files\Java\jdk1.8.0`, `C:\Program Files (x86)\Java\jre8`, or something of that sort.
+   - On a Mac, use the Finder to browse to the directory in which you've installed your preferred Java version. Type the name of the directory in the dialog's JRE Home field. My Mac has one Java directory named `/System/Library/Java/Java Virtual Machines/1.6.0.jdk/Contents/Home` and another Java directory named `/Library/Java/JavaVirtualMachines/jdk_1.8.0.jdk/Contents/Home`. (The first is for Apple's old version of Java; the second is for Oracle's new Java version.) You might also find Oracle's Java in the `/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home` directory.