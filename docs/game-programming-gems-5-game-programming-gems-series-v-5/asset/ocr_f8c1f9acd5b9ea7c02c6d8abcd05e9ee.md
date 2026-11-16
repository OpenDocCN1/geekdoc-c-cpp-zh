graphic, this function was placed in the menuScreen class for easy access. The background image stored in the parent class can be drawn during the call to the render function. Listing 1.17.1 shows the description of the menuScreen class.

# Listing 1.17.1 Description of the menuScreen Class

```
class menuScreen
{
public:
// menuReturn code
// The update method will return one of these codes to inform
// the menuManager of its status.
// NONE - no action, continue showing current menu
// NEXT - current menu should end and go to the next menu
// PREV - current menu should end and go to the previous menu
// POPUP - current menu is ending, display the menu menu
// PODUP - the menu is ending and popup menus are displayed
// END - This is the last menu and no menus are done
static enum menuReturn { NONE=0, NEXT, PREV, POPUP, END };
menuScreen(void);
virtual ~menuScreen(void);
// load all the resources needed for this menu
virtual bool init(void) = 0;
// called each frame to update the menu
virtual int update(BYTE keys[]) = 0;
// called each frame to draw the current menu
virtual void render(void) = 0;
// returns a string that represents the name
// of the next menu
std::string& getNextMenu(void);
protected:
// loads the background image
bool loadBackground(std::string imageName);
// all menus have a background image associated with them
resourceImage *bkgdImage;
// the name of the next menu
std::string nextMenu;
};
```

# Adding User Controls

User controls needed to gather input from the user are created with the menuControl class. MenuControl is implemented as an abstract class; all controls used in concrete menu classes will inherit their base functionality from this class.