This rung would set the output device on or off, depending on the current status (1 or 0) of variable #1100. Now, if the requirement is to switch on the device somewhere in the middle of program execution, wait for 5 seconds, and then switch it off and restart the execution, one may insert the following blocks in the program, at the desired place:

```
```text
#1100 = 1;
G04 X5;
#1100 = 0;
```
```

Unfortunately, this would not work. The output would indeed be turned on, but while performing the dwell for 5 seconds, the next macro statement (#1100 = 0) would be buffered and immediately executed, switching off the output instantly. Thus, even though the execution should dwell for 5 seconds, the output would switch on only momentarily. Therefore, in order to have the desired effect, it is necessary to suppress buffering in this case. This can be very simply done by inserting a blank NC statement (a semicolon, the EOB symbol, is treated as a blank NC statement) after the G04 block:

```
```text
#1100 = 1;
G04 X5;
;
#1100 = 0;
```
```

Fanuc control does not define a G-code to limit buffering to the desired number of blocks, unlike Haas control that has G103 for this purpose. However, as mentioned earlier, it is possible to define certain M-codes (in the range 0 to 255), for the sole purpose of preventing buffering of the following block. For example, if 100 is stored in any parameter in the range 3411 to 3420, M100 would prevent buffering of the following block. Then, instead of inserting a blank NC statement, in the previous example, M100 can be commanded. This method is better because a different programmer may consider the extra semicolon unnecessary, and may even choose to delete it! Note, however, that buffering should not be suppressed in radius compensation mode, because otherwise, the compensation would not be properly implemented by the control, resulting in incorrect machining.