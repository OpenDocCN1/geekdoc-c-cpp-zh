# # More RackAFX Controls and GUI Designer

RackAFX has several optional graphical user interface (GUI) controls that were not covered in the book chapters. It also has a GUI designer that lets you convert your slider-based default GUI into a fully customized version. The website www.willpirkle.com is always the best way to get the latest information on the GUI designer and any additional controls that may be added at a later date. The two additional GUI controls are the alpha wheel and liquid crystal display (LCD) and the vector joystick control.

# ## B.1 The Alpha Wheel and LCD Control

In the upper right of the main RackAFX UI is a control that represents an alpha wheel, LCD matrix view, and the control knob. During the course of designing your project, you've noticed that the LCD is used to give you feedback about the state of your project and compiler. However, it can also be used as a GUI control just like the other sliders. The LCD control allows you to store up to 1024 continuous slider controls inside it. Anything you can set up with a normal slider control will work as one of the LCD embedded controls. And, the GUI designer lets you place one of these controls on your own GUI. There are several uses for the control:

+   * It's a different way to store the continuous controls.
+   * If you run out of sliders, you can always put 1024 more of them in the LCD.
+   * You can use the enumerated list variable to create a set of presets or other global functions or configuration controls.

To set up the LCD control, right-click on it when you are in development mode (not with a plug-in loaded). A box pops up as shown in Figure B.1. Click on New to open the very familiar slider properties dialog. Fill it out just as you would any other slider control. After adding a few more controls, you might have something resembling Figure B.2, with three controls embedded. You can edit the controls, remove them, or move them up and down the list (which changes their sequence in the LCD control).

You treat these embedded slider controls just as any other slider, so there's nothing to add to your normal operational code. When you run your plug-in, use the alpha wheel to select one of the controls and the value knob to adjust its value. Note there is currently no edit control connected to the LCD for manual entry of control values. Figure B.3 shows the LCD control with the alpha wheel adjusted for the bass control.