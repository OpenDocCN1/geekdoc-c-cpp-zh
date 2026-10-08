
Since IB is used to connect the Referencing Outlet, you don't have to explicitly alloc/init the controls. Initialization is done in the View's awakeFromNib by calling a special function that initializes the stock control.

In this function, you set the control's index, min, max and default values with two flags, one for a volt/octave (logarithmic) control, the other to specify an integer display. By default, the background of the edit box is transparent, and the edit box is visible. You can alter this by using two methods and passing a boolean to toggle on or off:

```
(void)initControlWithName:(NSString*)name controlIndex:(int)index min:(float)min max:(float)maxV def:(float)defaultV voltOctave:(bool)vpo integerControl:(bool)intControl;
```

- (void)hideEditBox;
- (bool)hide;
- (void)setTransparentEditBoxBackground;
- (bool)transparent;

The knob has a drawing option—you can make a min-knob that is about 1/4 the size of the regular one by calling the method:

- -void)setMiniKnob;
- (bool)mini;

## Setting and Getting the Position of the Knob

You set the position of the knob (and text that is entered into the edit box) using the method:

- - (void)setValue;
(float)userValue;

The value you pass is in "user value," meaning it is not normalized as in VST3. This is the regular coated you use for your calculations.

A important aspect of the control is that it stores the zero-based index of the global parameter to which it is ultimately connected. It is set when you initialize the control. There are two accessor methods that the View will use to retrieve the index and control value when the knob is moved:

```
(int)controlID;
(float)controlValue;
```

The action handler for knob movements is WPRotaryKnobChanged the knob passes its id as the argument. The

![](img/b42d0dca53f4a889d8162d55f7c8c05d_153_0.png)

handler then uses the methods controlID and controlValue to alter the global parameter. In this way, handler can be used for all the knobs, and there is no decoding required for the controls its GUI parameter index.

If you want to modify {
control,
look at the

- - (IAction)WPrototaryKnobChanged:(id)sender

```
if([!sender respondsToSelector(@selector(controlID)]) ||
    ![sender respondsToSelector:@selector(controlValue)])
    return;
if([[sender controlID]) >= 0)
{
    // -- get the knob's user-value
Float32 floatValue = [sender controlValue];
    // -- use the value to create a Parameter
AudioUnitParameter param = (buddyAU, [sender controlID];audioUnitScope_Global, 0);
    // -- alter the Global parameter (explained below)
<SNIP SNIP SNIP>
}
```

initializer method initWithFrame in the .m file. Here you can see how to change the background and text color of the edit box as well as a few customizations. The knob images are stored in an array; there are 128 images depicting the knob in 128 different rotational positions. As you drag the mouse, a image is selected thereby animating the movement. Because discrete images are used, the shadows will also move properly. This can not be accomplished by simple image rotation. If you want to draw your own images, you can change the count of them with the #define statement at the top of the .m file:

```
#define KNOB_COUNT 128
```

The images are loaded into the array in the initializer. For our images, the file names are sequentially numbered so you use this scheme to get the file paths. Make sure you understand how to add resources to Xcode before you start modifying the images.

## 2.43 WPOptionMenuGroup

The WPOptionMenuGroup object consists of two controls: a static text label that is the control name and a NSPopUpButton which shows a list of strings in a menu. This is depicted in Figure 2.49. This control is half the height of the knob and the same width.

Figure 2.49: The WPOptionMenuGroup is also a cluster of controls.

The string list is zero-indexed and when the user selects a new string, an action handler is triggered. This control transmits an integer value representing the index of the string that is constantly selected. With the WPRotaryKnob, this control also stores the global parameter to which it is connected.

## NSTextField

### Filter

### NSPopUpButton

### LPF

### WPOptionMenuGroup

## Initialization

Since IB is used to connect the Referencing Object, you don't have to explicitly alloc/init the controls. Initialization is done in your' awakeFromNib method by calling a special function that initializes the control.

```
(void)initWithName:(NSString*) name
controlIndex:(int)index
enumString:(NSString*)enumStr
def:(float)defaultV
verySmallFont:(bool)smallFont;
```

You set the name with the first two arguments. The third is the "enumString," which is a comma-separated set of substrings like "LPF,BPF" that will populate the menu. The substrings are enumerated that LPF is 0, HPF is 1, etc. in this example. The default value is a float, but we do not use this in the host. The very small font is a flag may or not use depending on the host.

## Setting and Getting the Position of the Knob

- - (void)setValue;
(float)userValue;

The value you pass is in "user value," meaning it is not normalized as in VST3. This is the regular coated you use for your calculations.

A important aspect of the control is that it stores the zero-based index of the global parameter to which it is ultimately connected. It is set when you initialize the control. There are two accessor methods that the View will use to retrieve the index and control value when the knob is moved:

```
(int)controlID;
(float)controlValue;
```

The action handler for knob movements is WPRotaryKnobChanged the knob passes its id as the argument. The

handler then uses the methods controlID and controlValue to alter the global parameter. In this way, handler can be used for all the knobs, and there is no decoding required for the controls its GUI parameter index.

If you want to modify {
control,
look at the

- - (IAction)WPrototaryKnobChanged:(id)sender

```
if([!sender respondsToSelector(@selector(controlID)]) ||
    ![sender respondsToSelector(@selector(controlValue)])
    return;
if([[sender controlID]) >= 0)
{
    // -- get the knob's user-value
Float32 floatValue = [sender controlValue];
    // -- use the value to create a Parameter
AudioUnitParameter param = (buddyAU, [sender controlID];audioUnitScope_Global, 0);
    // -- alter the Global parameter (explained below)
<SNIP SNIP SNIP>
}
```

initializer method initWithFrame in the .m file. Here you can see how to change the background and text color of the edit box as well as a few customizations. The knob images are stored in an array; there are 128 images depicting the knob in 128 different rotational positions. As you drag the mouse, a image is selected thereby animating the movement. Because discrete images are used, the shadows will also move properly. This can not be accomplished by simple image rotation. If you want to draw your own images, you can change the count of them with the #define statement at the top of the .m file:

```
#define KNOB_COUNT 128
```

The images are loaded into the array in the initializer. For our images, the file names are sequentially numbered so you use this scheme to get the file paths. Make sure you understand how to add resources to Xcode before you start modifying the images.

## 2.43 WPOptionMenuGroup

The WPOptionMenuGroup object consists of two controls: a static text label that is the control name and a NSPopUpButton which shows a list of strings in a menu. This is depicted in Figure 2.49. This control is half the height of the knob and the same width.

Figure 2.49: The WPOptionMenuGroup is also a cluster of controls.

The string list is zero-indexed and when the user selects a new string, an action handler is triggered. This control transmits an integer value representing the index of the string that is constantly selected. With the WPRotaryKnob, this control also stores the global parameter to which it is connected.

## NSTextField

### Filter

### NSPopUpButton

### LPF

### WPOptionMenuGroup

## Initialization

Since IB is used to connect the Referencing Object, you don't have to explicitly alloc/init the controls. Initialization is done in your' awakeFromNib method by calling a special function that initializes the control.

```
(void)initWithName:(NSString*) name
controlIndex:(int)index
enumString:(NSString*)enumStr
def:(float)defaultV
verySmallFont:(bool)smallFont;
```

You set the name with the first two arguments. The third is the "enumString," which is a comma-separated set of substrings like "LPF,BPF" that will populate the menu. The substrings are enumerated that LPF is 0, HPF is 1, etc. in this example. The default value is a float, but we do not use this in the host. The very small font is a flag may or not use depending on the host.

## Setting and Getting the Position of the Knob

- - (void)setValue;
(float)userValue;

The value you pass is in "user value," meaning it is not normalized as in VST3. This is the regular coated you use for your calculations.

A important aspect of the control is that it stores the zero-based index of the global parameter to which it is ultimately connected. It is set when you initialize the control. There are two accessor methods that the View will use to retrieve the index and control value when the knob is moved:

```
(int)controlID;
(float)controlValue;
```

The action handler for knob movements is WPRotaryKnobChanged the knob passes its id as the argument. The

handler then uses the methods controlID and controlValue to alter the global parameter. In this way, handler can be used for all the knobs, and there is no decoding required for the controls its GUI parameter index.

If you want to modify {
control,
look at the

- - (IAction)WPrototaryKnobChanged:(id)sender

```
if([!sender respondsToSelector(@selector(controlID)]) ||
    ![sender respondsToSelector(@selector(controlValue)])
    return;
if([[sender controlID]) >= 0)
{
    // -- get the knob's user-value
Float32 floatValue = [sender controlValue];
    // -- use the value to create a Parameter
AudioUnitParameter param = (buddyAU, [sender controlID];audioUnitScope_Global, 0);
    // -- alter the Global parameter (explained below)
<SNIP SNIP SNIP>
}
```

## 2.44 The View Factory and CocoaView.plist

The View Factory is a simple object whose only real job is to load the view and pass it the AU pointer. However, you must get the name correctly tied to the GetProperty function to work. In addition, you need to setup the factory in a .plist file. The class definition for MiniSynthView is:

@class MiniSynthView;
@interface SynthFactoryBean : NSObject <AUCoUIView>

```
IBOutlet MiniSynthView *uiFreshlyLoaded;
```
