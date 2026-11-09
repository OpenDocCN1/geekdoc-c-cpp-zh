the cutting edges while also allowing the chips to be flushed out, at least as much as possible.

Virtually all CNC machining centers support two programming commands (fixed cycles) for peck drilling:

+   - G83 = Deep hole drilling
+   - G73 = High speed deep hole drilling

Take these descriptions as guidance only — a hole drilled in a tough material can be shallow and still benefit from this method of machining. High-speed peck drilling is a bit of an exaggeration, and some manuals actually call this G73 cycle *chip breaking cycle*, which is more descriptive. The *high speed* refers to the retract motion of G73 when compared to G83.

# **Programming Format**

Both G83 and G73 are common fixed cycles. Except the cycle number, their format is identical:

+   - G98/G99 G83 X.. Y.. R.. Z.. Q.. F..
+   - G98/G99 G73 X.. Y.. R.. Z.. Q.. F..

In both cases, the amount of Q is the *depth of each peck*. The difference between the two cycles is in the actual cutting, particularly in the retract motion after each peck:

*In the G83 cycle, the tool will retract to the R-level after each peck. In the G73 cycle, the tool will retract only by a certain minimum (~0.5 mm or 0.02\") after each peck.*

In both cases, the retract motion from the final depth will be either to the initial level (in G98 mode) or to the R-level (in G99 mode).

# **Application Notes**

The G83 cycle can be used for peck drilling of most holes, whereas the G73 cycle is better suited for holes that need chip