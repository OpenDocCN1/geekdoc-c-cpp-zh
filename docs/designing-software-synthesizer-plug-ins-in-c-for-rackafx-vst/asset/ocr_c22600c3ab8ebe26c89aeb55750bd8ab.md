# IController Controller::createSubController (UTFStringPtr* _name, UIDscription* description, VST3Editor* editor)

This is
the
only
code
you
need to
write—

```
// --- get the name string to test
ConstString name (_name);
```

```
// --- check the sub-controller name
if(name -- "VectorJoystick")
```

```
// --- get the X and Y parameter objects from our list
Parameter* jX = getParameterObject(VECTORJOYSTICK_X);
Parameter* jY = getParameterObject(VECTORJOYSTICK_Y);
```

```
// create the pad controller and pass it the X and Y
// parameter pointers
PadController* padController = new PadController(editor, this,
jsX, jY);
```

```
// --- return the newly created
return padController;
```

```
return NULL;
```

everything else is handled in VSTGUI and the PadController object.

# Part Two: GUI

Now you can open the VSTGUI editor in the VST3 client and add the new joystick control, or use the sample code with the control already added. The steps are:

+   - select the outer view to hold the control
- drag an instance of CXYPad into the container and position/size it as you wish
- go to the upper right of the editor to the Attributes section where you normally set the x,y coordinates, size and control-tag; in this case, instead of connecting the control to a control-tag, you connect it to a sub-controller that is at the bottom of the list; you simply type in the sub-controller name string "Vector.Joystick" as shown in Figure
11.25

That's all there is to creating the control; it will automatically update your X and Y parameters as the user moves the