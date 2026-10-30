In addition to the soft key functionality provided in the bada platform, a bada device usually also has some hard keys. There are default hard keys that perform critical tasks, such as **Power** and **Menu**, and optional hard keys that are device dependent, such as **Camera** and **Volume**. Figure R2.13 shows these keys on the bada Wave device.

![](bbox=[0.143, 0.207, 0.815, 0.421])

**Figure R2.13** Wave hardware keys overview.

This recipe assumes the steps detailed in the recipe ‘Add Soft Keys to a Form and Get Actions’ have been followed to add soft keys and soft key event handling to an application’s Form.

In this recipe the key events are received and an appropriate log message is printed to the output terminal.

As shown in the ‘Add Soft Keys to a Form and Get Actions’ recipe, the `MainForm` class is inherited from the `Form` base class and the `IActionEventListener` class is implemented to handle the soft key events. Hard key events are not received and handled in the same way as soft key events, and a separate listener interface must be implemented to receive key events. So additionally, the `MainForm` class must implement the `Osp::Ui::IKeyEventListener` interface class.

The following code snippet shows an example of the `MainForm` class definition:

```
class MainForm :
    public Osp::Ui::Controls::Form,
    public Osp::Ui::IActionEventListener,
    public Osp::Ui::IKeyEventListener
{

public:
    MainForm(void);
    ~MainForm(void);
    bool Initialize(void);

protected:
    static const int ID_SOFTKEY_LEFT = 101;
```