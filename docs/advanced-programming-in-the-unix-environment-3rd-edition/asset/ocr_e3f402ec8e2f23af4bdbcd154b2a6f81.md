BSD-derived platforms don’t support the ac_stat member, so we define the HAS_AC_STAT constant on the platforms that do support this member. Basing the defined symbol on the feature instead of on the platform makes the code read better and allows us to modify the program simply by adding the new definition to our compilation command. The alternative would be to use

```
#if !defined(BSD) && !defined(MACOS)
```

which becomes unwieldy as we port our application to additional platforms.
We define similar constants to determine whether the platform supports the ACORE and AXSIG accounting flags. We can’t use the flag symbols themselves, because on Linux, they are defined as enum values, which we can’t use in a #ifdef expression.
To perform our test, we do the following:

+   1. Become superuser and enable accounting, with the acct on command. Note that when this command terminates, accounting should be on; therefore, the first record in the accounting file should be from this command.
+   2. Exit the superuser shell and run the program in Figure 8.28. This should append six records to the accounting file: one for the superuser shell, one for the test parent, and one for each of the four test children.
+   A new process is not created by the exec l in the second child. There is only a single accounting record for the second child.
+   3. Become superuser and turn accounting off. Since accounting is off when this acct on command terminates, it should not appear in the accounting file.
+   4. Run the program in Figure 8.29 to print the selected fields from the accounting file.

The output from step 4 follows. We have appended the description of the process in italics to selected lines, for the discussion later.

```
acct on    e = 1, chars = 336, stat = 0:      S
sh         e = 1550, chars = 20168, stat = 0:   S
dd         e = 2, chars = 1585, stat = 0:      second child
a.out      e = 202, chars = 0, stat = 0:      parent
a.out      e = 420, chars = 0, stat = 134:  F   first child
a.out      e = 600, chars = 0, stat = 9:   F   fourth child
a.out      e = 801, chars = 0, stat = 0:  F   third child
```

For this system, the elapsed time values are measured in units of clock ticks. Figure 2.15 shows that this system generates 100 clock ticks per second. For example, the sleep(2) in the parent corresponds to the elapsed time of 202 clock ticks. For the first child, the sleep(4) becomes 420 clock ticks. Note that the amount of time a process sleeps is not exact. (We’ll return to the sleep function in Chapter 10.) Also, the calls to fork and exit take some amount of time.

Note that the ac_stat member is not the true termination status of the process, but rather corresponds to a portion of the termination status we have discussed in