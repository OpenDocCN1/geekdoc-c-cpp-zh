# Example 5-3 Configuring Router-Based TFTP Services for IP Phone Firmware

```
CME_Voice# dir flash:/phone/7940-7960
Directory of /phone/7940-7960/
98  -rw      129824 May 12 2008 21:33:56 -07:00 P0308000500.bin
99  -rw        458 May 12 2008 21:33:56 -07:00 P0308000500.loads
100 -rw      705536 May 12 2008 21:34:00 -07:00 P0308000500.sb2
101 -rw      130228 May 12 2008 21:34:00 -07:00 P0308000500.sbn
129996800 bytes total free
```

CME_Voice# configure terminal
Enter configuration commands, one per line. With CNTL/

```
CME_Voice()# tftp-server flash:/phone/7940-7960/P0308000500.bin alias
P0308000500.bin
CME_Voice()# tftp-server flash:/phone/7940-7960/P0308000500.loads alias
P0308000500.loads
CME_Voice()# tftp-server flash:/phone/7940-7960/P0308000500.sb2 alias
P0308000500.sb2
CME_Voice()# tftp-server flash:/phone/7940-7960/P0308000500.sbn alias
P0308000500.sbn
```

The alias syntax that follows the tftp-server command enables the firmware file to be requested by asking for the aliased filename. This is necessary in the newer CME versions, which organize the firmware files into subdirectories. The Cisco IP Phones do not know the path to the firmware file; they ask only for the firmware filename.

> **Note:** Be sure to make all the firmware files in each subdirectory via TFTP. The Cisco IP Phones use most, if not all, of these files during the boot process.

The firmware files for the Cisco 7940 and 7960 IP Phones are now available through TFTP from the Cisco Unified CME router. You can repeat this process as many times as necessary to make the firmware files available for the additional models of IP Phones you have on your network.

> **Note:** You can download the latest firmware files for Cisco IP Phones from the Cisco website assuming you have a valid support contract with Cisco. These files come in a TAR archive, which you can extract to the flash of your router with a single command.

# Base CME Configuration

For the CME router to support the Cisco IP Phones, you must configure some core telephony service information. The key items you must configure include the following:

+   - IP Source Address
- Max-DN
- Max-Ephones

![](bbox=[0.875, 0.905, 0.945, 0.955])