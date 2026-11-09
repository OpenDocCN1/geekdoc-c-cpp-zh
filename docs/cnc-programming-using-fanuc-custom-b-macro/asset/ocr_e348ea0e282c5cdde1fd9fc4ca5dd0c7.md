# CHAPTER 13

# Programmable
# Data Input

# 13.1  Introduction

This feature of a CNC machine is not really related to macro programming. It has been included in this text because it is an advanced programming feature which many programmers are not aware of, even though it is very useful and its use is pretty straightforward.

As the name suggests, *programmable data input*, which is commanded by G10, is used to write certain data into the control such as offset values and parameters. G10 is an optional feature on some control versions, which would need to be activated if its use is desired. This feature does not allow reading the current values of such data; one can only overwrite these.

The main applications of G10 are data input for the following:

+   - Offset distances for workpiece coordinate systems
+   - Offset distances for additional workpiece coordinate systems on a milling machine
+   - Compensation values on a milling machine (length and diameter)
+   - Compensation values on a lathe (radial/axial values, nose radius, and tip number)
+   - Parameter values

G10 can also be used to feed tool-management data such as tool life and offset number. This is, however, not discussed in this chapter, since it is not a very common application.

If the macro-programming feature is available on the machine, G10 is not needed in most cases. This is because system variables for all the offset distances and compensation values are available as read/write variables (refer to Sec. 3.5). In fact, system variables offer more flexibility, since the current values stored in them can also be read