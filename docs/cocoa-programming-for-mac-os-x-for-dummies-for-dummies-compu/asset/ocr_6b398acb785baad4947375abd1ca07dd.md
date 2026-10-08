5. Add the following actions to the `MyTextController` class:

+   - setBackgroundColor:
- setTextColor:
- toggleRuler:

![](bbox=[0.23, 0.26, 0.86, 0.53])

Figure 11-4:
Create a new class
to act as the
controller.

# ## Wiring the interface

To wire the components of your interface to the new `Controller` class, perform the following steps:

+   1. **Connect the outlets of `MyTextController` to the controls in the interface.**
    Control-drag from the XIB window `MyTextController` object to each of the four controls in turn, selecting the corresponding outlet from the black connections list overlay that appears. Figure 11-5 shows the `appleCheckbox` outlet connecting to the Apply to Selection check box.
2. **Connect the actions of the `MyTextController` object to the two ColorWells and the ruler check box.**
    To connect them, Control+drag from each control to the `MyText Controller` object. Figure 11-6 shows the `toggleRuler` action connected to its switch.
3. **Select the `MyTextController` class in the project window and choose File→Write Class Files to create the class files and add them to your project in Xcode.**