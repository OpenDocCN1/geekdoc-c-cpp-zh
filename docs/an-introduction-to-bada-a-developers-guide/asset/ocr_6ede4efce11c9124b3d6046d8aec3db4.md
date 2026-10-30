```
```cpp
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
```

The list of icons is created using the IconList control during the initialisation of the mainForm (`OnInitializing()`):

+   1. Create bitmaps for display in the IconList – a description of how to decode an image and store in a bitmap container can be found in the recipe ‘Add a Form to a Frame-based App’. **Note:** These bitmap containers must be deleted in the `OnTerminating()` method of the MainForm.
+   2. Create an instance of the IconList control.
+   3. Initialise the IconList object with the size and position of the control, the list style and the size of each icon.
+   4. Register the item event listener with the IconList control.
+   5. Remove the margins from the top and left side of the list.
+   6. Add the items to the IconList control.
+   7. Add the IconList control to the MainForm.

```
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
```
```