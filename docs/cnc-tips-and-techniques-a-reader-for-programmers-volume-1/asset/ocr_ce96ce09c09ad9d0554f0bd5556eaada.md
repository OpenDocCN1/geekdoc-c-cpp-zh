angle. **G62** may improve the surface finish when used to cut sharp inner corners in cutter radius offset mode. Its function is to automatically adjust the cutting feedrate. A tapping mode programmed with **G63** disables the feedrate override and the feed-hold button, and **G64** returns the cutting motions to their original programmed mode. Each mode selected replaces any other mode.

**G60** stands separately. Its purpose is to force a unidirectional tool positioning, regardless of which direction the tool comes from. It can be used to compensate for some minor backlash, but it does *not* remove it. Backlash problems require qualified service technicians.

There may be other G-codes not commonly used, but the ones mentioned in this column should provide some understanding of the more common special purpose G-codes.

![](bbox=[0.075, 0.501, 0.162, 0.545])

# ## Well-Structured Program Structure

*June 2006, updated February 2013*

A fairly experienced CNC user asked me recently, “*Are there any rules as to how actually write the program?*” His interest was in the format of the program, not its actual contents. He was interested if there are any preferable ways to structure a part program to gain certain advantages. Indeed, what is a good structure? In fact, what is a program structure in the first place?

A typical CNC program will contain several tools, arranged in the order of machining. Each tool will be programmed in three unique sections: 1) a few blocks at the *beginning* to move the tool to a cutting position, 2) the actual *machining* section, and 3) another few blocks to move the tool away from the work to make room for the next tool. No doubt, the machining section — the actual toolpath associated with cutting — is the most important one and is generally immune to any particular format. The beginning and the end of each tool are the areas where many