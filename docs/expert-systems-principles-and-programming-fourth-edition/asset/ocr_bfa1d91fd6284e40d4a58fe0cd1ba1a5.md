top of the file to make the code easier to understand and maintain, but the only enforced requirement is that the declaration is made at some point before the defunction requiring it is defined.

# Watching Deffunctions

When deffunctions are watched using the watch command, an informational message is printed whenever a deffunction begins or ends execution. For example:

```
CLIPS> (watch deffunctions)
CLIPS> (factorial 2)
DFN >> factorial ED:1 (2)
DFN >> factorial ED:2 (1)
DFN >> factorial ED:3 (0)
DFN << factorial ED:3 (0)
DFN << factorial ED:2 (1)
DFN << factorial ED:1 (2)
2
CLIPS>
```

The DFN at the beginning of the information message indicates that it relates to deffunctions. The >> symbol indicates that a deffunction is being entered and the << symbol indicates that a deffunction is being exited and the next symbol is the name of the deffunction being entered or exited, in this case the factorial deffunction. The ED symbol is short for “Evaluation Depth” and is followed by a colon and then the current evaluation depth, an integer. The evaluation depth is an indication of the nesting of deffunction calls. It starts at zero and then each time a deffunction is entered it increases by one. Each time a deffunction exits, it decreases by one. Finally the last piece of information displayed is the actual arguments to the deffunction.

In this example, the factorial deffunction is initially called with an argument of 2. The evaluation depth for this call is 1. The factorial deffunction must be called again to compute the factorial of 1. This call has an evaluation depth of 2 and an argument of 1. The next call is to compute the factorial of 0. This call has an evaluation depth of 3 and an argument of 0. Since the factorial deffunction does not need to recurse to determine the factorial of 0, the deffunction does not have to be called again and the nested deffunction calls can be exited. Each exit decrements the evaluation depth by 1 until the original deffunction call is exited and the value of 2 is returned.

It's also possible to watch specific deffunctions by adding their names to the end of a watch deffunctions command. For example:

```
CLIPS> (unwatch deffunctions)
CLIPS> (watch deffunctions C)
CLIPS> (A 2)
DFN >> C ED:3 (0)
```