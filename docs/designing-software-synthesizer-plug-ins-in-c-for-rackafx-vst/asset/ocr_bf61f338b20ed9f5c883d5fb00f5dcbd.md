Now practice setting up the Octave control—choose the integer datatype and the table to fill in the Slider Designer. Continuing through the table we find two enumerated controls. Let's practice setting up a radio button first.

#  2.10 Setting up Indexed Controls: Radio Buttons

Right click anywhere on the first radio button group that is the same row as the first sliders and a similar Radio Button Designer. You populate this in the same way, using the button to quickly advance through the rows. However, this has the Data Type fixed at enum. Entering the control name and UINT variable to link it with m (uFilterType), move to the box labeled “This list:” and enter the strings separated by commas. Since this is a C++ enumeration, you must be sure to use legal values for the sub-strings; for example your sub-string cannot start with a number, contain reserved characters like & *. If you compile and get an error that refers to enumeration, check your legality with the string names. If you need to change the enum string, do so in RackAFX.

On the left side of Figure 2.10 you can see a mock-up of the enumerated strings through input text. This is how you can make sure your strings do not flow outside the control (hint: use short meaningful strings). You can also see that this has index of 41.

#  2.11 Setting up Indexed Controls: Sliders

Continuing through Table 2.6 we find another filter type named FX Filter. This control uses the three sliders as the first filter type, LPF, HPF, BPF. You can put a slider control to act as an enumerated control. Right click on another slider group and choose enum from the data type list. The dialog box opens to reveal the string entry box and another list populated with the current enumerated strings. You can share these lists between controls by double-clicking the string in the lower box, which transfers the string into “This enum list:” Figure 2.11 shows the new Slider Designer. In enum mode, the high and low limits and default are not edited or usable.

#  2.12 Placing Controls Inside the LCD Control

![](bbox=[0.193, 0.597, 0.796, 0.903])

Figure 2.10: Configuring the radio button group is simple as the slider control.