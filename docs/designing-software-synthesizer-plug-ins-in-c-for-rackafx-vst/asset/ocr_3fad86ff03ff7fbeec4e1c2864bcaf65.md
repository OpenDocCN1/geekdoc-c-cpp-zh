RackAFX, when you hit the button, a dialog appears like the one shown in Figure 11.23.

Table 11.2: The CJoystickProgram functions you will be using.

# Figure 11.23: CJoystickProgram Selected Member Functions

| Function Name | Description |
| --- | --- |
| CJoystickProgram | Constructor |
| setSampleRate | set the sample rate for timing the program operation |
| startProgram | start the program at on time |
| resumeProgram | resume the program at off time if in sustain mode |
| incTimer | increment the program by one sample interval |
| getVectorMixValues | returns the A, B, C, D, AC-mix and BD-mix values |
| getVectorABCDMixes | returns only the AC-mix and BD-mix values |

RackAFX Vector joystick program awaiting programming.

You then follow a similar sequence as outlined in Figure 11.22 to program the rows:

+   1. select the first row by clicking on it

+   2. move the joystick to the location for vertex 0; you will see the mix values update in real time as you move the joystick

+   3. when satisfied with the location, click on the Time to Next Step cell and enter the duration in mSec for the first segment, then hit

+   4. this advances the selected row to the next one (you can always click on a row to select it too)

+   5. move the joystick to the next vertex and repeat from step 3

+   6. continue until you are done rows (you are not allowed to skip rows); on the last row, the Time to Next, you will enter only valid in loop, where the last vertex advances to the first in a hidden segment

You can use the <Clear Row> and <Clear Table> buttons to make edits to the rows.

You can program the joystick at development to create a preset, and also reprogram it at runtime while auditioning notes. This button and dialog are also available when you use the Make VST2 Compatible function and create a custom GUI—this is a drag-and-drop interface for joystick control on the GUI Designer page, so you can use the VS programmer in your VST2 synths.

# Using the CJoystickProgram

Once you've got a program set in development mode, you need to create and implement the object. In our synth

| Vector Joystick Program |
| Step | A Mix | B Mix | C Mix | D Mix | Time to Next Step (mSec) |
| --- | --- | --- | --- | --- | --- |
| 0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 1 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 2 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 15 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |

| Step Count: 0 |
| Clear Row | Clear Table | OK | Cancel |