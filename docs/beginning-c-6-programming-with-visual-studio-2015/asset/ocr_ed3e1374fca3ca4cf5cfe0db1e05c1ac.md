# TABLE 14-7: Other ComboBox Properties

| COMBOBOX PROPERTY | DESCRIPTION |
|---|---|
| Text | The Text property represents the text displayed at the head of the ComboBox. It is either an element of the list or a new text typed by the user. |
| SelectedIndex | Represents the index of the selected item in the list. If this is -1 then no selection is made. This is also the case if the user has typed something that was not in the list. |
| SelectedItem | Represents the actual item of the list, not just the index or the text. If nothing is selected or the user has typed something new, this returns null. |

# The TabControl

The TabControl is radically different than the other controls presented this section. It is a layout control that is used to group controls on pages that can be selected by clicking on them.

Tab controls are used when you want to display a lot of information in a single window but don’t want to clutter the view too much. In this case, you should divide the information into groups of related items and create a single page for each group. Generally speaking, you should never allow controls on one page to affect controls on another page. If you do so anyway, the user will not realize that something has changed on another page and will be confused when settings change behind her back.

By default each page is constructed of TabItems that, by default, are populated by a single Grid control, but you can change the Grid to any other control as you see fit. On each tab, you can lay out your UI and, by selecting the TabItems, you can change between the tabs. Each TabItem has a Header that can be used to display the tab itself. This can be used as a Content control, meaning that you can customize how the header is displayed so that it can be more than just a text.

# TRY IT OUT Designing the Options Window: KarliCards Gui \Options.xaml

The first thing that you probably notice when you see the Options window is that it looks remarkably like the About window, and that is true. Because of that, it is possible to reuse at least some of the code from the previous example.

+   1. Right-click the project in the Solution Explorer and chose Add Window. Name the window Options.xaml.
+   2. Delete the Grid control that is inserted by default.
+   3. Open the About.xaml window described earlier, copy the Grid control and all its content, and paste it into the new Options.xaml file.