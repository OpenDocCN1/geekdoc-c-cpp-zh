+   t: During an OP-phase this command will print the elapsed time since the OP-mode started.
+   x: Reset the hybrid controller.
+   X: Configure a crossbar switch module.¹⁷²
+   ?: Print help.

The following example shows how the hybrid controller can be controlled by manually issuing appropriate commands.¹⁷³ First, the OP- and IC-times are set to 500 and 100 milliseconds respectively as echoed by the controller (lines 1 to 4). Then a repetitive run is started by issuing an e-command which is eventually terminated by forcing the analog computer into HALT-mode (line 6). Then the digital output with address 0 is set to high before another repetitive run is started and later terminated by the h-command.

The command in line 10 reads the value from the computing element with the hexadecimal address 0160. The hybrid controller returns 0.0061 1, the first part being the value read while the second number is the identification number of the computing element being read.

Line 12 defines a readout group consisting of two computing elements with the respective hexadecimal addresses 0160 and 0161. Issuing an s-command returns complete status information of the hybrid controller also containing the addresses of all elements in the readout group. The f-command in line 16 reads all elements of this group and returns their values as -0.0004;-0.0002.

```
example.yml
1 c000500
2 T_OP=500
3 C000100
4 T_IC=100
5 e
6 h
7 DO
8 e
9 h
10 g0160
11 0.0061 1
12 G0160;0161.
13 s
14 STATE=NORM,MODE=IC,EXTH=DIS,OVLH=DIS,IC-time=100,OP-time=500,
```