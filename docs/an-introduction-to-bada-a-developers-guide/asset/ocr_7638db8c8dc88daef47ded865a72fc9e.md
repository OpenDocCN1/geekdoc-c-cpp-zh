In BuddyFix we will implement the following top-level Option menu items and sub-items:

| Buddies | Top-level item |
| Add Buddy | Sub-item, add a new buddy to the buddy list |
| Remove Buddy | Sub-item, remove a buddy from the buddy list |
| Pause sharing (if active) or Unpause sharing (if paused) | Top-level item, globally pause or unpause location sharing for all buddies |
| Settings | Top-level item, launch a Settings popup |
| About | Top-level item, launch an information popup providing app version and other information |

Let's look at the code.

Firstly in MainListForm.h, we add an OptionMenu pointer member pOptMenu, and event ID definitions:

```
class MainListForm :
    public Osp::Ui::Controls::Form
{
    // ...etc
    // Option Menu declarations

protected:
    Osp::Ui::Controls::OptionMenu* pOptMenu;
    static const int ID_OPTIONKEY = 100;
    static const int ID_OPTIONMENU_ITEM_1 = 101;
    static const int ID_OPTIONMENU_ITEM_2 = 102;
    static const int ID_OPTIONMENU_ITEM_3 = 103;
    static const int ID_OPTIONMENU_ITEM_4 = 104;
    static const int ID_OPTIONMENU_ITEM_5 = 105;
    static const int ID_OPTIONMENU_SUBITEM_1 = 201;
    static const int ID_OPTIONMENU_SUBITEM_2 = 202;
};
```

Next, in MainListForm.cpp, we add code to construct and assign the OptionMenu object. Event IDs are set by passing the ID to the item or sub-item constructor method. We must also invoke two Form methods:

```
SetOptionkeyActionId(ID_OPTIONKEY);
AddOptionkeyActionListener(*this);
```

The Form initialisation code now looks as below. Notice the use of two-phase construction to separately allocate and initialise the OptionMenu object: