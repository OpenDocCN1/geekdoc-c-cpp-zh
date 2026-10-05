Enter the following command to restrict the system to all processors except the first. In this system, the number of processors is 8, a full mask is 255 (0xff). Removing CPU 0 processes 254 (0xfe). Replace the mask with the correct one for your system.

# Cpu.exe -s 0fe

The view in Task Manager should look the same. Let's take a closer look at CPU 0. Run WPR again, and record a second time with the same settings as before.

Open the trace in WPA and navigate to Utilization by CPU.

Expand CPU 0. You should see CPUSTRES almost exclusively, with the System process appearing occasionally:

| CPU | Count | New Process |
|---|---|---|
| 0 | 15 | CPUSTRES.exe (18276) |
| 1 | 1 | CPUSTRES.exe (18276) |
| 2 | 1 | CPUSTRES.exe (18276) |
| 3 | 1 | CPUSTRES.exe (18276) |
| 4 | 1 | CPUSTRES.exe (18276) |
| 5 | 1 | System 4 |
| 6 | 1 | CPUSTRES.exe (18276) |
| 7 | 1 | CPUSTRES.exe (18276) |
| 8 | 1 | CPUSTRES.exe (18276) |
| | | | CPUSTRES.exe (18276) |

Notice in the CPU Usage (in View) (ms) column that the time spent in the system is very small (micro seconds). Clearly, CPU 0 is dedicated to the CPUSTRES process.

Run CPUSET with no arguments again. The first set (CPU 0) is marked Allocated: True because it's now allocated to a particular process and not for general system use.