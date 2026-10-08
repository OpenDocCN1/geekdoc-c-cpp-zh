The coordinates for each step are:

+   * 0: (0.0, 0.0) = 25% A, 25% B, 25% C, 25% D
* 1: (-1.0, 1.0) = 100% A
* 2: (1.0, 1.0) = 100% B
* 3: (1.0, -1.0) = 100% C
* 4: (-1.0, -1.0) = 100% D

For simplicity let's make the segment times 2 seconds each. The programming here is simply:

![](bbox=[0.325, 0.053, 0.518, 0.193])

![](bbox=[0.542, 0.053, 0.735, 0.193])

![](bbox=[0.762, 0.053, 0.955, 0.193])

![](bbox=[0.325, 0.246, 0.518, 0.386])

![](bbox=[0.542, 0.246, 0.735, 0.386])

![](bbox=[0.762, 0.246, 0.955, 0.386])

```
m_VPG.setProgramStep(0, 0.0, 0.0, 2000, false);
m_VPG.setProgramStep(1, -1.0, 1.0, 2000, false);
m_VPG.setProgramStep(2, 1.0, 1.0, 2000, false);
m_VPG.setProgramStep(3, 1.0, -1.0, 2000, false);
m_VPG.setProgramStep(4, -1.0, -1.0, 2000, false);
```

The last argument, which is the joystick coordinate flag—it is false because we are using rotated coordinates.

# Starting/Stopping

You start the program during a event with startProgram(). If the joystick is in sustain mode, it will pause itself once the vertex is hit (it's the second to last one in the program). When the note offen occurs, you resume operation with resumeProgram(), which takes the path through the last segment. If the program is not in sustain mode, then there is nothing to do here.

# Incrementing the Program

You have to increment the program on each sample interval to update the new vector mix. After incrementing the program, you can query it for the new vector mix values. These two steps always go together.

```
// --- some variables to hold the mix values float f, fB, fC, fD, fAC,
fBD;
m_VPG.incTimer();
// -- uses pass-by-reference to set ours with
values
m_VPG.getVectorMixValues(fA, fB, fC,
D);
```