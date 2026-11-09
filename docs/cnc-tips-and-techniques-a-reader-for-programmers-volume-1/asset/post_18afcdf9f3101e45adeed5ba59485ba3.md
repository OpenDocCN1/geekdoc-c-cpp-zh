
to the macro, which can also be modified to conventional type of machining.

The macro listing for the example with an accompanying figure appears in Appendix 3 at the end of this book.

![](img/0023bd5cc50494e6d7799ab76d437c8d_187_0.png)

## Scaling Option
*September 2008, updated February 13*

One function on many control systems is called scaling. Often offered as an optional control feature, scaling allows an existing program to machine a part smaller or larger. Before you jump to conclusions, keep in mind that scaling is not meant to be the means of part correction due to poor programming methods or bad setup. Scaling is often used in casting or plastic injection mold work to allow adjustments due to shrinkage during the molding process, but can be used in 2D work as well. From a CNC programmer’s perspective (rather than engineering perspective), scaling is quite easy to program, but there are a number of special considerations.

### Changing the Toolpath

Scaling will physically change the current toolpath proportionally, based on the location of the scaling center and the scaling factor provided. A control-dependent system parameter can be set to make scaling effective or ineffective for each of the three main axes, but not for any additional axis. Also, scaling does not affect various offset modes, namely work offsets G54–G59, tool length offset G43, and cutter radius offset mode G41–G42. If a fixed cycle in the G81–G89 series, or G73, G74, or G76, is used while scaling mode is active, the shift amount in G76 and G87 cycles (the peck drill depth and relief amount in G73 and G83 cycles) will *not* be affected.

The *machine zero return* commands are another consideration. Preparatory commands related to the machine zero return, particularly G28 and G30, but also G27 and G29 (rarely used anymore), should always be programmed with scaling mode OFF in effect. On older controls that still use the G92 command for position register, make sure the scaling mode OFF is also in effect. Cutter radius offsets G41 and G42 should always be canceled by G40 before the scaling function is activated. As mentioned already, other commands and functions can be active, including all work offset commands G54 through G59 and the additional ones, if they are available.

### G50 and G51 Codes

Fanuc programming format uses two G-codes: G50 and G51 commands, where G50 cancels the scaling mode and G51 makes the scaling mode active. The programming format for G51 is:

```gcode
G51 I.. J.. K.. P..
```

IJK addresses refer to their respective XYZ coordinates of the scaling center, while the P-address is the scaling factor. Scaling center is defined in absolute coordinates of the current units of measurement, and scaling factor can be in 0.001 or 0.00001 increments, depending on the control setting. In order to prevent any conflict, both G50 and G51 should be programmed as separate blocks, with no other significant data included.

The scaling center determines the *location* of the scaled tool path and the scaling factor determines its size. For scaling factors greater than one, the machining tool path will be *expanded*. For scaling factors smaller than one, the machining tool path will be *reduced*. The scaled part will always expand away from or reduce towards the scaling point equally along all specified axes.

The basic programming format is illustrated in the following example:

```gcode
N1 G20
N2 G17 G40 G80
N3 G50 (SCALING OFF AT TOOL START)
N4 G90 G00 G54 X-1.25 Y-1.25 S800 M03
N5 G43 Z1.0 H01 M08
N6 G51 I0 J0 P1.050 (SCALING CENTER AT X0Y0 - 1.05X expand)
N7 G01 Z-0.7 F50.0
N8 G41 X-0.75 D51 F25.0
N9 Y1.75 F15.0
N10 X1.5
N11 G02 X2.5 Y0.75 I0 J-1.0
N12 G01 Y-0.75
N13 X-1.25
N14 G40 Y-1.25 M09
N15 G50 (SCALING OFF AT TOOL END)
N16 G00 Z1.0
N17 G28 Z1.0
N18 M30
%
```

## Rounding Errors

One very important consideration in scaling is a possible rounding error. To illustrate, consider a conversion between metric and inch units. A dimension of 1.0 inch will become 25.4 mm, which is an exact conversion. On the other hand, 25.4 mm converted to inches will use a factor of 0.039370079. If the scaling factor is set to a three decimal accuracy, the 25.4 mm will become only 0.991 inches (25.4 x 0.039 = 0.9906) — a rather large error of about 0.009. With scaling factor set to five decimal places, the error will still be there but it will be practically negligible.

The scaling factor is a *multiplying factor*, not a percentage. If a certain scaling percentage is required — for example, 5% shrinkage — it has to be converted. The scaling factors of P1.05 (expansion) or P0.95 (reduction) are well within the expected accuracy of the final part precision.

For a complete example with illustration, using the scaling function, see Appendix 4 at the back of this book.

![](img/0023bd5cc50494e6d7799ab76d437c8d_190_0.png)

## Safety and CNC Programming
*October 2008, updated February 2013*

When it comes to safety in machine shops, the great majority adheres to the occupational safety laws and regulations of the jurisdiction in which they are located, often exceeding the official ones. Common rules are generally well known. They include wearing protective clothing, safety boots, safety glasses with protective side shield, keeping the environment clean, removing any hazards, and many others. Machining safety is paramount to the successful operation of any machinery, CNC equipment included. Many safety issues are associated with the actual equipment operation and machining of a part. Very few companies have standards relating to safety issues in CNC programming, whether manual or computer generated. CNC programmers may work from an office environment, yet they have a great responsibility to build safety features into every CNC program.

A fairly long list can be assembled to identify what such features should be. A lot depends on the product manufactured, the equipment used, and company standards and culture. Certain general approach to safety in CNC programming can be identified, regardless of local conditions or method of programming. A short list focused on CNC vertical machining centers can be adapted to CNC lathes and other machines, and may include the following items:

- **Approach program development with safety in mind for all work.**
  
  This underlying philosophy should be constant for any part, any program, and any machine.

- **Program your approach towards a part in the XY axes first; then move the Z-axis.**
  
  When the tool moves above the part first, it is less likely to come into collision with the part itself or the fixture. In terms of efficiency, it takes longer than three-axis simultaneous motion, but this XYZ split motion can always be changed after a safe setup had been established.

- **Program a retraction from a part in the Z axis first, then move the XY axes.**
  
  Tool retraction from a part may include only the Z-axis, but for XYZ motion, the split is safer than three-axis motion. This is the opposite of the previous item.

- **Start every program with an initial setting and cancellations (so-called status block or a safety block).**
  
  It is usual to include various settings and cancellations at the beginning of a program. Settings may include dimensional units selection, plane selection, and absolute mode whereas cancellations typically include fixed cycles, cutter radius and length offset, and initial status of certain options (for example, scaling off or polar coordinates off).

- **Provide sufficient clearances (above part, below part, lead-ins, and lead-outs, etc.).**
  
  Insufficient clearances are often the cause of dangerous tool-machine collisions. Rapid motion to a certain depth may be safer if programmed as two motions: above the part first, then to the required depth. This method helps during setup and does not increase cycle time during automatic operation.

- **Program reasonable speeds, feeds, depth of cuts, width of cuts, etc.**
  
  Every CNC machine has override switches — establishing speeds and feeds on the conservative side may be safer, although less efficient. Efficiency can be achieved by optimizing the program at the machine during setup, using the overrides. This approach may be particularly useful when working with less experienced operators.
