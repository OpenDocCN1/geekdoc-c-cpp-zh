| Cisco IOS output | Explanation |
|---|---|
| ```text
R1#show secure bootset
IOS resilience router id FHK1028517C
IOS image resilience version 12.4 activated at 09:02:03 UTC Sun Jul 1 2012
Secure archive flash:c1841-advipservicesk9-mz.124-20.T1.bin type is image (elf) []
    File size is 37081324 bytes, run size is 37274008 bytes
    Runnable image, entry point 0x8000F000, run from ram
IOS configuration resilience version 12.4 activated at 09:02:12 UTC Sun Jul 1 2012
Secure archive flash:
runcfg-20120701-090211.ar type is config
configuration archive size 3160 bytes
``` | Display the status of Cisco IOS image and configuration resilience. This step is important to verify that the Cisco IOS image and configuration files have been properly backed up and secured.<br><br>Of importance to note are the location and filenames of both files (for example, flash:c1841-advipservicesk9-mz.124-20.T1.bin and flash:runcfg-20120701-090211.ar). |

# Restoring Bootset Files

To restore a primary bootset from a secure archive after the router has been tampered with (by an NVRAM erase or a disk format), you must complete four steps.

The following example walks through the process of restoring bootset files to an ISR with a corrupt IOS that boots to ROMMON mode.

| Command | Description |
|---|---|
| ```text
Router#reload
Proceed with reload? [confirm]
rommon 1 > dir flash:
``` | Reload the router. Press **Enter** to continue.<br><br>Enter ROMMON mode and display the bootset files. |
| ```text
rommon 2 > boot c1841-advipservicesk9-mz.124-20.T1.bin
``` | Boot the router using the listed image. |
| ```text
Router(config)#secure boot-config
restore flash:runcfg-20120701-090211.ar
``` | Restore the secure configuration to the archive found in flash. |