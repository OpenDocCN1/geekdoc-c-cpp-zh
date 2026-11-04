# Complete the following form to generate a cron tab line

Ctrl-click (or command-click on the Mac) to select multiple entries

![](bbox=[0.15, 0.24, 0.9, 0.62])

Figure 16.3 Configure to schedule at 11:00 a.m. and 4:00 p.m

+   - Click Save output to file and enter myfile so the output will be stored in file myfile.
+   - Click the button Generate Cron tab Line.
+   - You should see the generated line as shown in Figure 16.4, which is:

```
0 11,16 * * * myscript.sh >myfile
```

![](bbox=[0.35, 0.75, 0.7, 0.9])

Figure 16.4 The generated line

The tool also displays sample dates and times that the script file will be scheduled to run. It is clear from Figure 16.4 that the script file myscript.sh will run at 11:00 a.m. and 4:00 p.m. every day.