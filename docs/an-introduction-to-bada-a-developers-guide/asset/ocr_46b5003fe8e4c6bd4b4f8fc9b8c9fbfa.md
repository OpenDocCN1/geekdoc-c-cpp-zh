A user can interact with their bada device using a variety of different gestures (motion UI) and can rotate the display so that the orientation of the application changes. This recipe details the steps to enable motion and orientation control within an application and describes the code that needs to be implemented for the Form to receive and handle motion and orientation changed events.

The three types of motion events supported are:

+   - Double-tap: Occurs when any part of the device is tapped twice. Tapping uses the acceleration sensor, so any part of the device can be tapped, including the screen.
+   - Shake: Occurs when the device is quickly moved back and forth multiple times. Shake can last a long time. To accurately capture this behaviour, both the start and the end of shake are reported as two separate events.
+   - Snap: Occurs when the device is moved along one axis and back.

This recipe assumes the steps detailed in the recipe ‘Add a Form to a Frame-based App’ (which you can find in the second group of recipes, “UI Basics”) have been followed to add a Form to the application’s Frame.

In this recipe a Flash animation is created and played on the display. The user can control the state of the animation, the visibility, and the size and position of the animation by using motion events.

As shown in the ‘Add a Form to a Frame-based App’ recipe, the MainForm class is inherited from the Form base class. For this form to handle motion and orientation events the motion and orientation event listener interfaces have to be implemented. So in this recipe the MainForm class must implement the Osp::Ui::IMotionEventListener and the Osp::Ui::IOrientationEventListener interface classes.

The following code snippet shows an example of the MainForm class definition:

```
class MainForm :
    public Osp::Ui::Controls::Form,
    public Osp::Ui::IMotionEventListener,
    public Osp::Ui::IOrientationEventListener
{
public:
    MainForm(void);
    ~MainForm(void);
    bool Initialize(void);

protected:
    Osp::Ui::Motion* pMotion;

public:
    Osp::Ui::Controls::Flash* pFlash;

    result OnInitializing(void);
```