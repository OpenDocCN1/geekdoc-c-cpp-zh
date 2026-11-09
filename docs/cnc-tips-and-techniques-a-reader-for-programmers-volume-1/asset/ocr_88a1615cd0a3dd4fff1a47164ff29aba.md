![](bbox=[0.07, 0.11, 0.156, 0.15])

# Create Your Own G-Code

*August 2008, updated February 2013*

Custom macros are a very common method of enhancing the concept of subprograms by adding variable data and many data manipulation features. One of the less frequently used macro features involves the development of customized G-codes. Typically, a custom G-code for machining will be some kind of a cycle and will appear as such in the program. G65 statement can also be used, but it does not provide the same transparency. The macro example used in this essay will recreate the G13 command used on some controls other than Fanuc. As the actual control model is very important, the macro will be developed for Fanuc 16 /18 /21 systems.

# The G13 Command

Preparatory command G13 is commonly used to machine a circular pocket, such as a counter bore or a spot face, in climb milling mode. The macro will be stored as a cycle using only three major tool motions:

+   - Motion 1: Lead-in arc —180 degrees from the circular pocket center
+   - Motion 2: Full circle machining
+   - Motion 3: Lead-out arc —180 degs. back to the circular pocket center

As cutter radius commands G40 / G41 / G42 cannot be applied on an arc, they will not be used. Yet, the macro will still allow the CNC operator to fine tune the pocket dimensions at the machine, following established procedures as with a cutter radius offset. Development will start the same way as for any G65 macro call. Three variable arguments will be required:

+   - Circular pocket diameter — argument C (#3 in macro)
+   - Tool offset number to store the cutter radius — argument D (#7 in macro)
+   - Cutting feedrate — argument F (#9 in macro)