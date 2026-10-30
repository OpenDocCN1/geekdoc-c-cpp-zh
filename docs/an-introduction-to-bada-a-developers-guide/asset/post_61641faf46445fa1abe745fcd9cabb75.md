
## Step 1: Create the BaseForm class

The first step is to create a BaseForm that can be used to display the tabbed Forms. As the functionality of each of the nine Forms is the same in this recipe, it is more efficient to create a single Base Form and pass in any customisation for it in the Initialize() method.

The following code snippet shows an example of the BaseForm class definition:

```cpp
class BaseForm :
    public Osp::Ui::Controls::Form,
    public Osp::Ui::IActionEventListener
{
public:
    BaseForm(void);
    ~BaseForm(void);
    bool Initialize(int actionId);

protected:
    static const int ID_SOFTKEY_RIGHT = 110;

private:
    int id;

public:
    static const int ID_TAB_ONE = 100;
    static const int ID_TAB_TWO = 101;
    // ...
    static const int ID_TAB_NINE = 108;

    result OnInitializing(void);
    result OnTerminating(void);

    void OnActionPerformed(const Osp::Ui::Control& source,
        int actionId);
};
```

In the Initialize() method the BaseForm is constructed as a normal Form with a title area, indicator area, tab area and a right soft key, and the passed in actionId is stored in a member variable for later use:

```cpp
bool
BaseForm::Initialize(int actionId)
{
    Form::Construct(FORM_STYLE_NORMAL|FORM_STYLE_TITLE|
        FORM_STYLE_INDICATOR|FORM_STYLE_SOFTKEY_1|
        FORM_STYLE_TEXT_TAB);

    id = actionId;

    return true;
}
```

The tab control is created, with the right soft key, within the BaseForm’s OnInitializing() method:

1. Set the text for the right soft key.
2. Assign the soft key `actionId` and register the soft key event listener.
3. Get the pointer to the `BaseForm`’s tab control.
4. Add the tab items to the tab control – in this recipe the tab controls contain text labels.
5. Set the selected tab index, using the `actionId` parameter passed in to the `Initialize()` method.
6. Register the action event listener with the tab control.

```cpp
SetSoftkeyText(SOFTKEY_1, "Back");
SetSoftkeyActionId(SOFTKEY_1, ID_SOFTKEY_RIGHT);
AddSoftkeyActionListener(SOFTKEY_1, *this);

Tab* pTab = GetTab();
if(pTab)
{
        // Add the tabs
        pTab->AddItem(L"One", ID_TAB_ONE);
        pTab->AddItem(L"Two", ID_TAB_TWO);
        // ...
        pTab->AddItem(L"Nine", ID_TAB_NINE);

        // Set the selected tab
        pTab->SetSelectedItem(
                pTab->GetItemIndexFromActionId(id));

        // Add the action event listener
        pTab->AddActionEventListener(*this);
}
```

The event handling for the soft key and for navigating between the tabs is described later in Step 6.

## Step 2: Create the MainForm class

The `MainForm` displays a list of icons. Depending on which icon the user selects, the relevant tabbed Form will be displayed.
The following code snippet shows an example of the `MainForm` class definition:

```cpp
class MainForm :
    public Osp::Ui::Controls::Form,
    public Osp::Ui::IItemEventListener
{
public:
    MainForm(void);
    ~MainForm(void);
    bool Initialize(void);

protected:
    static const int ID_ICON_LIST_ITEM1 = 121;
    static const int ID_ICON_LIST_ITEM2 = 122;
    // ...
    static const int ID_ICON_LIST_ITEM9 = 129;

    Osp::Graphics::Bitmap* pBitmapNormal1;
    Osp::Graphics::Bitmap* pBitmapNormal2;
    // ...
    Osp::Graphics::Bitmap* pBitmapNormal9;

    result CreateBitmaps(void);
    result DeleteBitmaps(void);

public:
    result OnInitializing(void);
    result OnTerminating(void);

    void OnItemStateChanged(const Osp::Ui::Control& source,
                            int index, int itemId, Osp::Ui::ItemStatus status);
};
```

The list of icons is created using the IconList control during the initialisation of the mainForm (`OnInitializing()`):

1. Create bitmaps for display in the IconList – a description of how to decode an image and store in a bitmap container can be found in the recipe ‘Add a Form to a Frame-based App’. **Note:** These bitmap containers must be deleted in the `OnTerminating()` method of the MainForm.
2. Create an instance of the IconList control.
3. Initialise the IconList object with the size and position of the control, the list style and the size of each icon.
4. Register the item event listener with the IconList control.
5. Remove the margins from the top and left side of the list.
6. Add the items to the IconList control.
7. Add the IconList control to the MainForm.

```cpp
CreateBitmaps();

// Create Icon List
IconList* pIconList = new IconList();
pIconList->Construct(Rectangle(0, 0, GetClientAreaBounds().width,
                               GetClientAreaBounds().height),
                     ICON_LIST_STYLE_NORMAL, 160, 160);
pIconList->AddItemEventListener(*this);

// Remove margins from top and left of the icons
pIconList->setMargin(0, 0);

// Add the icons to the list
pIconList->AddItem(null, pBitmapNormal1, null,
    ID_ICON_LIST_ITEM1);
pIconList->AddItem(null, pBitmapNormal2, null,
    ID_ICON_LIST_ITEM2);
// ...
pIconList->AddItem(null, pBitmapNormal9, null,
    ID_ICON_LIST_ITEM9);

// Add icon list control to the Form
AddControl(*pIconList);
```

In this recipe, the default focus animation provided by the IconList control is used when an item is selected. Alternatively, a specific bitmap can be used to indicate the focus, by adding a focused bitmap parameter in the AddItem() method. If a focused bitmap is used, the default focus animation must be disabled by calling the IconList::SetFocusAnimationEnabled() method with the enable parameter set to false.

The event handling for icon selection is described in Step 5.

## Step 3: Create the FormMgr class

The FormMgr is a Form control that is used to manage the creation and display of all the Forms in the application; it does not display any controls itself. Requests from the MainForm or from the BaseForms are sent to the FormMgr using the Control class's SendUserEvent() method.

The following code snippet shows an example of the FormMgr class definition:

```cpp
class FormMgr :
    public Osp::Ui::Controls::Form
{
public:
    FormMgr(void);
    virtual ~FormMgr(void);
    bool Initialize(void);

protected:
    Osp::Ui::Controls::Form* pPreviousForm;
    MainForm* pMainForm;

public:
    virtual result OnInitializing(void);
    virtual result OnTerminating(void);
    static const RequestId REQUEST_MAINFORM = 100;
    static const RequestId REQUEST_ITEM1 = 101;
    static const RequestId REQUEST_ITEM2 = 102;
    // ...
    static const RequestId REQUEST_ITEM9 = 109;
    bool SetStarterForm(RequestId requestId,
        Osp::Base::Collection::IList* pArgs);

    void SwitchToForm(RequestId requestId,
        Osp::Base::Collection::IList* pArgs);

    void OnUserEventReceivedN(RequestId requestId,
        Osp::Base::Collection::IList* pArgs);
};
```

In the Initialize() method the FormMgr is constructed as a normal Form and given the name 'FormMgr'. The name is important, because it is used by the MainForm and the BaseForms to identify the control to send user events to:

```cpp
bool
FormMgr::Initialize()
{
    Form::Construct(FORM_STYLE_NORMAL);
    Form::SetName("FormMgr");

    return true;
}
```

When a user event is received from either the MainForm or any of the BaseForms, the OnUserEventReceivedN() method is called. In this method the SwitchToForm() method is called to process the event:

```cpp
void
FormMgr::OnUserEventReceivedN(RequestId requestId,
    Osp::Base::Collection::IList* pArgs)
{
    SwitchToForm(requestId, pArgs);
}
```

The SwitchToForm() method is responsible for the creation and display of the requested Form. In this recipe the MainForm is created only once and exists throughout the lifetime of the application, but the BaseForms are created and destroyed as required.

For each BaseForm display request the following steps are performed:

1. Create an instance of a BaseForm and initialise it, passing in the relevant actionId.
2. Set the text to be displayed in the BaseForm's Title area.
3. Add the BaseForm to the application's Frame.
4. Set the BaseForm as the current Form of the Frame.
5. Draw and Show the Form.
6. Remove the previous BaseForm control and store a reference to the current BaseForm.

A MainForm display request follows the same steps, with the exception that if it already exists it does not need to be created and added to the application frame again.
