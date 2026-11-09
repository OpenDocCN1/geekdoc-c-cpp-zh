# ## Speeds and Feeds

For a safe machining operation, identifying the spindle speeds and cutting feedrates in the program helps to make intelligent decisions when using spindle and feedrate overrides, particularly for the initial part. As an operator, keep in mind that even the most experienced programmer may not always be exact with speeds and feeds. In fact, optimizing speeds and feeds at the machine is often one of the most important functions of a CNC operator.

This example uses one spindle speed of 900 rpm (S900) and one feedrate of 200 mm/min (about 8 ipm). Some milling jobs may have two or more feedrates applied to the same tool.

Spindle rotation is also important. When interpreting a part program, three M-functions relate to spindle rotation: M03 (CW), M04 (CCW), and M05 (spindle stop). M03 is the standard rotation for right hand tools whereas M04 is used for left hand tools.

# ## Tool Numbers

Many errors at the machine happen because of wrong tool selection. In the example, the tool number is identified by the address T. Its meaning is determined by the type of automatic tool changer (ATC). For the fixed type ATC, each tool returns to the same magazine pocket it came from; the address T indicates both the pocket number and the tool number. In case of the more common random type ATC, the address T identifies the tool to be used next.

There are two T addresses in the ex.: one in block N2 (T07) and the other in block N4 (T10). Note that the block N3 contains ATC function M06. Once the tool change has been completed, the control searches for T10 to be ready in the magazine. To interpret these three blocks, T07 means get tool number 7 ready for tool change, M06 means get T07 to the spindle, and T10 means get the next tool T10 ready. Having the next tool ready is one of the greatest advantages of the random type automatic tool changer.