# MENU

The Menu control displays a main menu for a window. The Menu can provide submenus, shortcuts (such as [Ctrl]+O for the Open command), and accelerators (e.g., opening the File menu when you press [Alt]+F).

The Menu contains MenuItem objects that represent the commands in the menu. You can build submenus by placing MenuItems inside other MenuItems.

When the user selects a menu item, the corresponding MenuItem object raises its Click event. Your program can catch and handle that event as it handles Button Click.

The MenuItem's Header property determines what it displays. The Header value is simple text. Place an ampersand in front of the Header's letter that you want the MenuItem to use as an accelerator. For example, if you set the Header to File, then the MenuItem displays File (Note that this is different from the way Windows Forms handles this. In a Windows Forms application, you place an ampersand in front of the character that you want to underline in a menu).

# ACTIVATING ACCELERATORS

In recent Windows operating systems, accelerator characters are not normally underlined until the user presses the [Alt] key. Then the accelerator characters are underlined, and the user can press the corresponding key to trigger it.

In a typical application, for example, when the user presses [Alt], the File menu's underline appears. If the user presses F, the menu shows its items with accelerator keys underlined. In many programs, the File menu contains a New command. If the user presses N while the accelerators are visible, that command executes.

To set a menu item's shortcut keys by using the MenuItem's InputGestureText property. For example, you set the InputGestureText for the New command to [Ctrl]+N.

Support for accelerators is automatic. You only need to define the accelerator by adding underscores, and the application automatically does the rest.

Unfortunately, support for shortcuts is not automatic, your program must catch the appropriate keystroke and take action when necessary. WPP provides a command architecture that allows you to handle shortcuts for menu items in a general way, but since it is fairly complicated, it isn't described in any more detail here. Chapter 19, "Commanding," covers commands completely.

Figure 7-9 shows a program with its File menu. In this figure, I pressed [Alt] and F to open the File menu.

![](bbox=[0.598, 0.723, 0.866, 0.911])

FIGURE 7-9