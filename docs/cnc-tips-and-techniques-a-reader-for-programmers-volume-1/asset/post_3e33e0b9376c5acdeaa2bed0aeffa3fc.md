
On the other hand, the control features may be a lot more significant, particularly if *Machine A* has a different control make than *Machine B*. For example, Fanuc, Yasnac, and Haas controls are programmed in a similar way, but they also have their own differences. The programmer has to know *all* features of both controls and consider *all* control options available.

Normally, a program is developed for a particular combination of machine and control. Being able to switch the job from *Machine A* to *Machine B* or vice versa for scheduling reasons, or if one machine is down, often means changing the program. Yet, for controls that belong to the same group (such as Fanuc, Yasnac, Haas, and many others), a program can be written in such a way that it reflects the common denominator of the machines and controls. It may not always be possible to switch machines without any program changes, but minimizing such changes goes a long way towards improvement in productivity.

### Addressing Machine Differences

To address the machine design differences in the program, some ideas may be worth considering. When assigning tool numbers and their corresponding offset numbers for commonly used tools, assign those numbers that are common to both machines, typically in the low numbers. If the top spindle speed is required, consider programming the top speed of the machine that has the *lower* maximum. The same will apply for feedrates, although maximum feedrate is not commonly programmed and should not be an issue. Random type and fixed type of automatic tool change can be resolved in program structure (see below). Special features unique to one machine only cannot be compromised.

In programming structure, the first change may be right at the program beginning. When programming a startup block, its typical contents may be N1 G20 G17 G40 G18 G49 or similar. Some controls require that the unit selection command G20 (or G21) is in a separate block. Placing the G20 or G21 in a block by itself will work for all types of controls.

Similar structural change may reflect the tool change. Although it is customary to program **T02 M06**, for example, in the same block, some controls require that each command is in its own block. Again, using the two block method will always work. When using M-functions, most older controls only accept one in a block, newer controls may accept up to three. This convenience may work against the ability to select an alternate machine, so using a single M-function in a block provides a better program structure for that purpose.

There are other programming tools, some not always available. The most typical of them are the block skip function (slash) common to all controls, and the macro feature that is optional on most controls. Using a block skip method can be very powerful, particularly if the control allows the slash code in the middle of the block. In that case, for example, programming **S5000 M03 / S6000** in the same block will rotate the spindle at 5000 rpm if block skip is *ON*, and 6000 rpm if the switch is *OFF*. Note that both controls must have this special feature. Also note the inclusion of M03 *in front* of the slash.

Manipulating the program structure to achieve a certain result can be very useful. Ideally, programming for a single machine/control combination is preferred. Selecting an alternate machine because of an emergency will generally justify the changes required in the program. Selecting an alternate machine for scheduling reasons requires a certain compromise in programming and even machine setup. Understanding the possibilities will result in better decisions.

![](img/0023bd5cc50494e6d7799ab76d437c8d_79_0.png)

## Standard and Rigid Tapping — Part 1

*December 2005, updated February 2013*

In this two-part essay, we look at the two common methods of producing tapped holes on CNC machining centers. In this first part, the focus will be on tapping using floating tap holders whereas the second part will cover the subject of rigid tapping.

Tapping operation on conventional mills, lathes, and CNC machines has been one of the basic operations to machine holes. To this day, with all its disadvantages, one of the most common methods of tapping uses special tapping heads, known as the *tension-compression* type. Another term for this type of tool is a *floating tap holder*.

### Standard Tapping Method

In a typical tension-compression tap holder, the tap is held firmly so it cannot fall out, but loose enough to provide axial flexibility upon entering a drilled hole. A thread in the hole is formed by the size and shape of the tap. Although still very popular, floating tap holders present one major problem — they make it difficult to maintain precise thread depth, particularly in blind holes.

### Basic Principles

The main principle of standard tapping is the synchronization of spindle speed and tapping feedrate. That is achieved by multiplying the spindle speed (r/min) by the tap lead (pitch), resulting in the feedrate per minute. At the beginning of the cut, the tap has to accelerate from zero feedrate to a rather heavy feedrate. The time required to reach the programmed feedrate is called *acceleration*. In order to reach the programmed feedrate before any contact with the material, the tap must start further away from the hole — this is the R-level in fixed cycles. As the tap enters the hole, it encounters a resistance, and the tap is pushed slightly into the holder (using its compression capabilities). When the tap reaches the hole bottom and the spindle stops, the deceleration of the spindle forces the tap to be slightly pulled out of the tool holder (using tension of the holder).

A Reader for Programmers

Standard tapping is almost always programmed using one of two tapping cycles: G84 (right hand tapping) and G74 (left hand tapping). As you will find in the second part of this essay, many control systems support the same format for rigid tapping either as provided or slightly modified. The major difference is not much in the programming technique as it is in machine design and suitable tooling.

### Why Underfeed?

Most experienced CNC programmers have faced various tapping problems in their careers. The floating tap holder is an imperfect tool to say the least. It is a mechanical device and, as such, subject to some variables, including spindle fluctuations. If the tapping operation is not successful the first time (assuming the program is correct in principle), programmers often use a simple technique for a quick fix: tapping feedrate reduction. This reduction is called underfeeding because it is lower than the normal tapping feedrate, which is always r/min x pitch. Here are the reasons why this technique often works.

Most spindles may fluctuate up to ±10 r/min, particularly at high speeds. Because the tapping feed is always a direct relationship between the spindle speed and the tap pitch, any spindle fluctuation throws this relationship out of balance. When the tap in a floating holder enters the hole, it is pushed a bit into the holder, before the tap has a chance to “bite” into the material. This is the compression part of tapping. When a tap reaches the Z-depth, the spindle stops, but not right away; it has to wind down first. In order not to break the tap, the floating holder allows the tap to be pulled slightly out of the holder by its own force, after the Z-axis motion stopped. This part is called tension. Compression means pushing; tension means pulling. Now back to the spindle fluctuation.

CNC Tips and Techniques

Take a floating tap holder and try to push, then pull, the part that holds the tap. It is much easier to pull it out than push it in. In technical terms, it means tension presents fewer, if any, problems. In order to eliminate thread damage upon tap entry or exit, the feedrate can be reduced by 2% to 5%, anywhere between 98% and 95% of the nominal tapping feedrate. In this case, the tap is pulling from the tap holder and compensates for the spindle speed differences.

Keep in mind that a slight underfeeding when using floating tap holders is not always a solution to better tapping, but it may be the quickest solution in certain cases.

Floating tap holders are on the way out. Although they have served the industry for many years, a newer technology has become the standard. Since the introduction of rigid tapping in the early 1990s, the tapping methods and techniques have changed dramatically. The column covers the subject of rigid tapping.
