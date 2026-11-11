```
```java
// demonstrate icons

MenuItem cutItem = new MenuItem("Cut",
    new ImageView("menu/cut.gif"));
MenuItem copyItem = new MenuItem("Copy",
    new ImageView("menu/copy.gif"));
MenuItem pasteItem = new MenuItem("Paste",
    new ImageView("menu/paste.gif"));

// demonstrate context menu

ContextMenu contextMenu = new ContextMenu(cutItem, copyItem, pasteItem);
textArea.setContextMenu(contextMenu);

editMenu.getItems().addAll(cutItem, copyItem, pasteItem);
    // Bug or restriction—must add to context menu first
    // http://bugs.java.com/bugdatabase/view_bug.do?bug_id=JDK-8194270

// demonstrate nested menus

Menu optionsMenu = new Menu("Options",
    new ImageView("menu/options.gif"), readOnlyItem,
    insertItem, overwriteItem);

editMenu.getItems().add(optionsMenu);

// demonstrate mnemonics

MenuItem aboutProgramItem = new MenuItem("About this program");
MenuItem aboutCoreJavaItem = new MenuItem("About Core Java");
Menu helpMenu = new Menu("Help", null,
    aboutProgramItem, aboutCoreJavaItem);

// add menu bar

MenuBar bar = new MenuBar(fileMenu, editMenu, helpMenu);
VBox root = new VBox(bar, textArea);
for (Menu menu : bar.getMenus()) defaultAction(menu, event ->
{
    MenuItem item = (MenuItem) event.getSource();
    textArea.appendText(item.getText() + " selected\n");
});

stage.setScene(new Scene(root));
stage.setTitle("MenuTest");
stage.show();
}
}
```
```