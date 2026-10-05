5. Open Task Manager, click the Performance tab, and select the CPU label.

6. Change the CPU graph view to show individual processors (if the view is configured for overall utilization).

7. At the command window, run the following command, replacing the number after -p with the ID of the CPUSTRES process on your system:

```
CpuSet.exe -p 18276 -s 3
```

The -s argument specifies the processor mask to set as the default for the process. Here, 3 means CPU 0 and 1. You should see Task Manager hard at work on these two CPUs:

![](bbox=[0.216, 0.29, 0.676, 0.473])

8. Let's look at CPU 0 more closely to see what threads it's running. For this, you'll use Windows Performance Recorder (WPR) and Windows Performance Analyzer (WPA) from the Windows SDK. Click the Start button, type WPR, and select Windows Performance Recorder. Then accept the exception prompt. You should see the following dialog box:

![](bbox=[0.216, 0.574, 0.706, 0.903])