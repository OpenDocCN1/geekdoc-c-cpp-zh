+   2. Click **System and Security** and then click **System**. This opens the System Properties dialog box, which you can also access by right-clicking on **Computer** in Explorer and selecting **Properties**.

+   3. Click **Advanced System Settings**.

+   4. In the Performance area, click **Settings**. This opens the Performance Options dialog box.

+   5. Click the **Advanced** tab.

+   6. In the Virtual Memory area, click **Change**.

# EXPERIMENT: Viewing page file recommended sizes

To view the actual variables calculated in Table 5-12, follow these steps (this experiment was done using x86 Windows 10 system):

+   1. Start local kernel debugging.

+   2. Locate Smss processes:

```
1kd> lprocess 0 smss.exe
PROCESS 8e54bc40 SessionId:none Cid:0130 Peb:02bab000 ParentCid:0004
  DirBase: biffe0020 ObjectTable:8a767640 HandleCount:<Data Not Accessible>
  Image: smss.exe
```

```
PROCESS 9985bc40 SessionId:1 Cid:01d4 Peb:02f9c00 ParentCid:0130
  DirBase: biffe0080 ObjectTable:00000000 HandleCount:0.
  Image: smss.exe
```

```
PROCESS a122bc40 SessionId:2 Cid:02a8 Peb:02fcd00 ParentCid:0130
  DirBase: biffe0320 ObjectTable:00000000 HandleCount:0.
  Image: smss.exe
```

+   3. Locate the first one (with a session ID of none), which is the master Smss.exe. (Refer Chapter 2 for more details).

+   4. Switch the debugger context to that process:

```
1kd> .process /r /p 8e54bc40
Implicit process is now 8e54bc40
Loading User Symbols...
```

+   5. Show the four variables described in the previous section. (Each one is 64 bits in size).

```
1kd> dq smss|SmpDesiredSizeBasedOnRAM L1
PROCESS 00974cd0 00000000'4fff1a00
```