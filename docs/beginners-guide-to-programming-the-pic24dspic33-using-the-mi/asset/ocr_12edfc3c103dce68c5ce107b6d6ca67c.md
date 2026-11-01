# One Hundred Year Clock Calendar Demo

![](bbox=[0.15, 0.13, 0.9, 0.54])

Figure A-10: Clock Demo.

Depressing pushbutton S3 initializes Clock demo. This demo enters a mode where pushbuttons assume clock setting and control operations for internal 100 year real time clock calendar. User options are: change mode from clock display to clock setting and enter clock changes, stay in clock mode to simply display clock, or exit clock mode back to "Flash Screens". In order for this demo to work you must have a 32 KHz crystal and two 33 pF capacitors connected to pins 11 and 12 of the PIC24F. The Experimenter provides this functionality. Designated button functions are as follows:

+   - Push Button S1 toggle between clock run mode and clock setting mode
+   - Push Button S2 if in clock setting mode increment current data field
+   - Push Button S3 if in clock setting mode decrement current data field
+   - Push Button S4 advance to next allowable data field if in clock setting mode or if pressed in clock run mode exit to "Flash Screens"