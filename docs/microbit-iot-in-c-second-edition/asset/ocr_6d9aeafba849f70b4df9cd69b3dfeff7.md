Examining the data reveals that for the micro:bit V1, short pulses returned 6
 long returned 16, both plus or minus 1. Thus the threshold is
approximately 11. For the micro:bit V2 the values are around 20 for a short
pulse and 60 for a long, giving 40 as a reasonable choice of threshold.

With a threshold set we can classify the pulses into short and long and store
zeros and ones in the buffer:

```
int threshold=11;
//threshold=40;// uncomment for V2
int buf[41];
int j;
for (int i = 0; j < 41; j++) {
  for (i = 1; i < 200; i++) {
    if (P0.getDigitalValue() == 1)break;
  }
  for (i = 1; i < 200; i++) {
    if (P0.getDigitalValue() == 0) break;
  }
  buf[j] = 0;
  if (i > threshold)buf[j] = 1;
}
```

You can afford to include this extra processing in the data collection loop
because it happens while the line is low and we aren't interested in
measuring this time accurately.

**If you try this you will discover that it doesn't work.** Not only does it
drop bits, it seems to drop the same bits each time you run the program. This
is a particular problem for the microbit V2, which never manages to
complete a reading correctly. This suggests that it is a systematic effect and
the result of random noise.

The cause of the problem is, in fact, the system timer interrupt. The entire
transaction takes about one interrupt interval and, as the timer is
started when the program starts, the interrupt occurs at the same point
time you run the program - hence the regularity. The solution is to turn off
interrupts for the duration of the regularity. Turning off interrupts for any length
time is not a good idea, but for the short time that the reading is being
it causes no serious problems.