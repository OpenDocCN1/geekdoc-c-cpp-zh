```
static const int ID_SOFTKEY_RIGHT = 102;

Osp::Ui::KeyCode prevKeyCode;
Osp::Ui::KeyState prevKeyState;

public:
    result OnInitializing(void);
    result OnTerminating(void);

    void OnActionPerformed(const Osp::Ui::Control& source,
        int actionId);

    void OnKeyPressed (const Osp::Ui::Control &source,
        Osp::Ui::KeyCode keyCode);
    void OnKeyReleased (const Osp::Ui::Control &source,
        Osp::Ui::KeyCode keyCode);
    void OnKeyLongPressed (const Osp::Ui::Control &source,
        Osp::Ui::KeyCode keyCode);
};
```

To receive key events the MainForm must register the key event listener in the OnInitializing() method, using the AddKeyEventListener() method:

```
// Register MainForm with key event listener
AddKeyEventListener(*this);
```

To handle the key events when they occur the following methods must be implemented by the MainForm: OnKeyPressed(), OnKeyReleased(), and OnKeyLongPressed(). Each method is passed information about the source of the event and the key code of the hard key the event is related to.

The following code snippets show examples of these methods:

```
void
MainForm::OnKeyPressed(const Control &source,
    Osp::Ui::KeyCode keyCode)
{
    switch(keyCode)
    {
    case Osp::Ui::KEY_SIDE_UP:
        AppLog("Side key up pressed \n");
        break;
    case Osp::Ui::KEY_SIDE_DOWN:
        AppLog("Side key down pressed \n");
        break;
    case Osp::Ui::KEY_CAMERA:
        AppLog("Camera key pressed \n");
        break;
    case Osp::Ui::KEY_SWITCH:
        AppLog("Task switcher key pressed \n");
        break;
    default:
        AppLog("Invalid key pressed \n");
        break;
    }
    prevKeyCode = keyCode;
    prevKeyState = KEY_PRESSED;
```