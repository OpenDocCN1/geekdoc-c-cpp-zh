```
#1 = #1 * 20;
```

(This calculates the multiplication factor, as defined in Table 5.2(b), for the current coordinate system. In our example, #1 would store 60)

(#1 would store 521, 5241, 5261, 5281, 5301, and 5321, corresponding to G54, G55, G56, G57, G58, and G59, respectively, depending on which one is the current coordinate system. The stored value would be the variable number corresponding to the X-axis offset value for the current coordinate system, as shown in Table 3.12/Table 5.2(a). In our example, #1 would store 5261)

(#5021 contains the tool’s current X-coordinate in MCS, and #5201 contains the X-external offset. As already explained, when the difference in their values is stored in the system variable corresponding to the X-offset of a WCS, the current position of the tool becomes the new X-datum of that WCS, that is, the current tool position gets redefined as X0 in WCS. In our example, #5261 would get appropriately modified, which would shift the X-datum for G56 to the current X-position of the tool)

(Shifts datum for the Y-axis to the current Y-position of the tool. In our example, #5262 would get appropriately modified, which would shift the Y-datum of G56)

```
#1 = #1 + 5201;
```

```
#[#1] = #5021 - #5201;
```

```
#[#1 + 1] = #5022 - #5202;
```

```
M30;
```

Note that this program has been written without making a flowchart. A flowchart is not needed for straightforward cases such as this. Although the algorithm in this program is very simple:

+   1. Identify the current workpiece coordinate system.
+   2. Identify the system variables for X- and Y-work offset values corresponding to this coordinate system.
+   3. Redefine the identified system variables, using the given formulae.

However, even if one decides to write a program without making a flowchart, at least the algorithm must be noted down in black and white, before attempting to write the program. This would be useful for future reference also, as a quick intuitive interpretation of a macro program is generally not possible due to its abstract look.