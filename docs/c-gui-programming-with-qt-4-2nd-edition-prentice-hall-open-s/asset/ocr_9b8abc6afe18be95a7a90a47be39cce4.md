```
editMenu->addAction(cutAction);
editMenu->addAction(copyAction);
editMenu->addAction(pasteAction);
editMenu->addAction(deleteAction);
```

```
selectSubMenu = editMenu->addMenu(tr("Select"));
selectSubMenu->addAction(selectRowAction);
selectSubMenu->addAction(selectColumnAction);
selectSubMenu->addAction(selectAllAction);
```

```
editMenu->addSeparator();
editMenu->addAction(findAction);
editMenu->addAction(gotoCellAction);
```

We create the Edit menu, adding actions with QMenu::addAction() for the File menu, and adding the submenu with QMenu::addMenu() at the position where we want it to be. To add the submenu, like the menu it belongs to, a QMenu

```
toolsMenu = menuBar()->addMenu(tr("Tools"));
toolsMenu->addAction(recalculateAction);
toolsMenu->addAction(sortAction);
```

```
optionsMenu = menuBar()->addMenu(tr("Options"));
optionsMenu->addAction(showGridAction);
optionsMenu->addAction(autoRecalcAction);
```

```
menuBar()->addSeparator();
```

```
helpMenu = menuBar()->addMenu(tr("Help"));
helpMenu->addAction(aboutAction);
helpMenu->addAction(aboutQtAction);
}
```

We create the Tools, Options, and Help menus in a similar fashion. We insert a separator between the Options and Help menus. In Motif and C styles, the separator pushes the Help menu to the right; in other styles, the separator is ignored. Figure 3.5 shows both cases.

# ### Figure 3.5. The menu bar in Motif and Windows styles

| File | Edit | Tools | Options | Help |
| File | Edit | Tools | Options | Help |