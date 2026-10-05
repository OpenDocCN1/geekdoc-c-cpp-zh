
The single line controlling our camera uses the Vector3.Lerp function to interpolate the camera's transform position to that of the target stored in followTarget. We add an offset to the position (so that we end up above the target rather inside it) and use the speed multiplied by Time.deltaTime to interpolate independent of frame rate.

It is a very simple camera that one works well for basic top-down games.

Note that in the Lazer Blast Survival example for this book, an empty gameObject named CamTarget is used as the camera target. It is positioned in front of the player, parent to the player, so it inherits the player's rotation. By positioning a target object in front of the player for use with a top-down camera like this, it can help gameplay by providing a better view of the player rather than centering on the screen.

## 4.7 Input Scripts

In Chapter 3, we saw that the main player structure contained a single input script designed to take keyboard input. Adding input systems is a case of building custom input scripts that follow a similar format, so that the existing player code need not to be changed to accommodate different controls.

It may be required to take input from other methods than the keyboard, such as a mouse or a joystick. You can easily set up alternate controls in the Unity editor via the Edit -> Project Settings

### 4.7.1 Mouse Input

The Mouse_Input.cs script calculates the movement of the mouse between each frame and uses it for input.

Below is the script:

```
public class Mouse_Input : BaseInputController
{
    private Vector2 prevMousePos;
    private Vector2 mouseDelta;

    private float speedX = 0.05f;
    private float speedY = 0.1f;

    public void Start()
    {
        prevMousePos = Input.mousePosition;
    }

    public override void CheckInput()
    {
        // get input data from vertical and horizontal axis and
        // store them internally in vert and hor so we don't
// have to access them every time we need to relay input
// data out
```

```
// calculate a percentage amount to use per pixel
float scaleX = 100 / Screen.width;
float scaleY = 100 / Screen.height;
```

```
// calculate and use delta
float mouseDeltaY = Input.mousePosition.y - prevMousePos.y;
float mouseDeltaX = Input.mousePosition.x - prevMousePos.x;
```

```
// scale based on screen size
vert += (mouseDeltaY * speedY) * scaleY;
horz += (mouseDeltaX * speedX) * scaleX;
```

```
// store this mouse position for the next time we're here
prevMousePos = Input.mousePosition;
```

```
// set up Boolean values for up, down, left and right
Up = (vert > 0);
Down = (vert < 0);
Left = (horz < 0);
Right = (horz > 0);
```

```
// get fire / action buttons
Fire = Input.GetButton("Fire");
```

```
public void LateUpdate()
{
// check inputs each LateUpdate() ready for the next tick
CheckInput();
}
```

### 4.7.1.1 Script Breakdown

The Start() adds a default value to prevMousePos, which will be used to calculate the movement between each update. If prevMousePos was left at 0 (its default), the first time CheckInput() happens, the script will incorrectly assume that the mouse has moved from 0 to the current mouse position.

Input provides an interface to Unity's input systems. It is used for everything from gyrometer input on mobile devices. Input.mousePosition delivers the current position of the mouse in pixel coordinates as a 2D vector, with the bottom left of the screen at 0,0 and the top right at Screen.width, Screen.height.

```
public void Start()
{
prevMousePos = Input.mousePosition;
}
```

The input scripts use CheckInput() as their default main update function, is intended to be called from the player class.

The mouse input system uses mouse delta movement (the amount of movement since the last update) instead of mouse position. The delta amount is converted into a percentage (a percentage of a screen width or height), and the resulting value is used as input.

CheckInput() starts by calculating a value to work at. The floats scaleX and scaleY hold the equivalent of the screen's width and height, respectively:

```
public override void CheckInput()
{
    // get input data from vertical and horizontal axis and
    // store them internally in vert and hor so we don't
    // have to access them every time we need relay input
    // data out

    // calculate a percentage amount to use per pixel
    float scaleX = 100 / Screen.width;
    float scaleY = 100 / Screen.height;
```

The delta amount of mouse movement is calculated in the code by taking the current position and subtracting it from the position that the mouse was at the end of the last update:

```
// calculate and use deltas
float mouseDeltaY = Input.mousePosition.y - prevMousePos.y;
float mouseDeltaX = Input.mousePosition.x - prevMousePos.x;
```

When the mouse position is multiplied by scale variables (scaleX and scaleY), we end up with a percentage amount. We say that the mouse is at a percentage across the screen and use that amount as:

```
// scale based on screen size
vert += (mouseDeltaY * speedY) * scaleY;
horz += (mouseDeltaX * speedX) * scaleX;
```

```
// store this mouse position for the next time we're here
prevMousePos = Input.mousePosition;
```

The mouse-based input scripts also populate variables for directional, if required:

```
// set up Boolean values for up, down, left and right
Up = (vert > 0);
Down = (vert < 0);
Left = (horz < 0);
Right = (horz > 0);
```

To make the fire button work properly, it must be set up correctly in the input settings of the Unity editor, under the Fire entry:

```
// get fire / action buttons
Fire = Input.GetButton("Fire");
}
```

The script calls its own update function from Late(), which is where all input checking happen:

```
public void LateUpdate()
{
// check inputs each Update ready for the next tick
CheckInput();
}
```

Note that if firing does not work after applying this script, check that Unity is set up correctly to receive mouse input. To do this, open Unity's Input menu (Edit -> Project Settings -> Input) and check that the Axes entry for Fire contains an entry either in the negative, positive, or buttons.

### 4.7.2 Single Axis Keyboard Input

The single axis input script takes away the vertical axis and only takes input from horizontal and fire inputs. It follows the same format as the other input scripts and the input script from Chapter 3 (Player Structure), except the vertical axis is excluded:

```
public class Single_Axis_Keyboard_Input : BaseInputController
{
    public override void CheckInput()
    {
        // get data from vertical and horizontal axis and
        // store them internally in vert and hor so we don't
        // have to access them every time we need relay input
        // data out
        horz = Input.GetAxis("Horizontal");

        // set some Boolean values for up, down, left and right
        Left = (horz < 0);
        Right = (horz > 0);

        // get fire / action buttons
        Fire = Input.GetButton("Fire");
    }

    public void LateUpdate()
    {
        // check inputs each LateUpdate() ready for the next tick
        CheckInput();
    }
}
```

## 4.8 Automatic Self-Destruction Script

The main use for a script that automatically destroys its gameObject is for special effects. Particle effects such as explosions will be instantiated, their effect will play out, and then they need to be destroyed.

In the example games, a short and simple class called AutomaticDestroyObject is attached to a gameObject. After a set amount of time, set in the Unity Inspector window, the gameObject is destroyed along with any child objects attached to it.

Below is the full script:

```
public class AutomaticDestroyObject : MonoBehaviour
{
    public float timeBeforeObjectDestroys;

    void Start () {
        // the function DestroyGO() will be called in
        // timeBeforeObjectDestroys seconds
        Invoke("DestroyGO", timeBeforeObjectDestroys);
    }

    void DestroyGO() {
        // destroy this gameObject
        Destroy(gameObject);
    }
}
```

### 4.8.1 Script Breakdown

The class, which derives from MonoBehaviour, is very simple. It uses Invoke to schedule a call to the DestroyGO() function at a time set by the public variable timeBeforeObjectDestroys. It probably goes without saying that DestroyGO() takes care of destroying itself, with Destroy(gameObject).

## 4.9 Automatic Object Spinner

One common action you may need to spin an object. This may be for a number of reasons, the most obvious (in this book, at least) being to draw attention to power-ups in the Interstellar Paranoids game. By spinning the power-ups, they are more obvious to the player as something that may be interacted with, whereas static power-ups may be easily missed or ignored.

Making an object spin in Unity may be very simple, but having a script to take care of this is a useful tool to keep in the toolkit.

Below is the script in:

```
using UnityEngine;
using System.Collections;
```