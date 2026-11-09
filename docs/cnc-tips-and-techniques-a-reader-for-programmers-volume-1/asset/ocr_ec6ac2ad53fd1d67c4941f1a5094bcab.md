The individual addresses are pretty straightforward — X is the thread final diameter, Z is the final position for the thread length, I is equal to zero, unless you’re cutting a tapered thread, K is the actual thread depth, D is the first depth of the thread, A is the thread angle, and F is the thread lead as feedrate. The P option is not available on all controls; its purpose is to control the actual cutting motions of the tool. As good as this cycle was, and still is, it lacks certain features that could make the life of a CNC operator a bit easier. Consider the quick changes that can be done at the machine, in a rush to improve a thread on the fly, so to speak. There are only two: 1) changing the D to control the number of passes and 2) changing the A to control the infeed angle. That’s it. All other minor adjustments were not readily possible, unless you got into the system parameters, and that is a territory forbidden to many.

# Improving G76

Fanuc realized the need to improve this very powerful cycle, and made it even more powerful by adding certain features that can now be set right at the machine control, rather than through various system parameters. The result was a two-block G76 — yes, two blocks! — applicable to controls such as Fanuc 0,16,18,21, and a number of others. This format offers much more than the two features that can be changed at the machine. Is there a price to pay for this added convenience? Yes, but a rather small one. The G76 has to be repeated in both blocks. In addition, the programmers have to understand the meaning of each data entry within the cycle. Here is the format for a two-block G76 threading cycle:

```
G76 P.. Q.. R..
G76 X.. Z.. R.. P.. Q.. F..
```

Note the repetition of P/Q/R in both blocks — they are the reason for having two blocks in the first place. Needless to say,