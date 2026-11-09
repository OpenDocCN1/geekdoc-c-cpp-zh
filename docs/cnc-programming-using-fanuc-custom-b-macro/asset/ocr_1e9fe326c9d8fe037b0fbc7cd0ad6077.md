Wear offset correction for the Z-axis can be done in a similar manner, which is left as an exercise (usually, radial wear is more serious than the axial wear). One would need to touch a known Z-surface (which has been faced by the tool to be probed), and determine the error. The program for both internal and external tools would be the same in this case. The Z-axis wear offset system variables belong to #2100 series for 64 offsets, and #11000 series for 99 offsets (refer to Tables 3.2 and 3.3).

In order to use macro O8023, it would need to be called immediately after machining by the tool, for which wear adjustment is to be done. It is possible to continue machining further, with the new wear offset values. In fact, in the case of suspected inaccuracy, a single straight-turning command, with a small depth of cut, can be given first. The main machining codes can be given after calling this macro. This would automate the inspection and correction process. One may use this technique after, say, every 10 parts, which would ensure virtually zero rejection. The number of machined parts, in the current machining session, gets stored in system variable #3901 (refer to Sec. 3.5, subsection Number of Machined Parts). The main program may call/skip the probing macro by

```
<set-up commands>
<straight turning>
IF [#3901 LE 10] GOTO 100;
G65 P8023 T_ X_ Z_ D_;
#3901 = 0;
N100;
<machining program>
M30;
```

where the part count is reset to zero whenever the macro is called. It is left as an exercise for the reader to think how to implement the same logic if the part count variable #3901 is not to be reset (since it may be desired to keep track of the total number of the machined parts in the current machining session).

The arguments of macro call for O8023 pass data for the following:

+   - T (#20) = four-digit tool code for the probe
+   - X (#24) = diameter to be probed
+   - Z (#26) = axis position where probing is to be done
+   - D (#7) = diameter of the probe ball

Though one can develop macros for specific probing requirements, the probe manufacturers usually supply probes with software for common probing applications.