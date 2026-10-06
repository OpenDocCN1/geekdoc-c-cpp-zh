
file() slot, which we will implement in the next section. This connection ensures when the user chooses the FileNew menu item, clicks the New toolbar button, or presses Ctrl+N, the newFile() slot is called.

The Open, Save, and Save As actions are very similar to the New action, so we will skip directly to the "recently opened files" part of the File menu:

```
for (int i = 0; i < MaxRecentFiles; i++) {
    recentFileActions[i] = new QAction(this);
    recentFileActions[i]->setVisible(false);
    connect(recentFileActions[i], SIGNAL(triggered()),
        this, SLOT(openRecentFile()));
}
```

We populate the recentFileActions array with actions. Each action is hidden and connected to the openRecentFile() slot. Later, on will see how the recent file actions are made visible and used.

```
exitAction = new QAction(tr("E&exit"), this);
exitAction->setShortcut(tr("Ctrl+Q"));
exitAction->setStatusTip(tr("Exit the application"));
connect(exitAction, SIGNAL(triggered()), this, SLOT(close()));
```

The Exit action is slightly different from the ones we have seen so far. There is no standardized key sequence for terminating an application, so here we specify the key sequence explicitly, and that we connect to the window's close() slot, which is provided by Qt.

We can now skip to Select All action:

```
selectAllAction = new QAction(tr("&All"), this);
selectAllAction->setShortcut(QKeySequence::SelectAll);
selectAllAction->setStatusTip(tr("Select all the cells in the 
"spreadsheet\"));
connect(selectAllAction, SIGNAL(triggered()),
    spreadsheet, SLOT(selectAll()));
```

The selectAll() slot is provided by one of QTableWidget's ancestors, QAbstractItemView, so we do not have to implement it ourselves.

Let's skip further to the Show Grid action in the Options menu:

```
showGridAction = new QAction(tr("&Show Grid"), this);
showGridAction->setCheckable(true);
showGridAction->setChecked(spreadsheet->showGrid());
showGridAction->setStatusTip(tr("Show or hide the spreadsheet's \grid\"));

connect(showGridAction, spreadsheet, SIGNAL(oggled(bool)), SLOT(showGrid(bool)));
```

Show Grid is a clickable action. Checkable actions are rendered with a check-mark in the menu and implemented as toggle buttons in the toolbar. When the action is turned on, the Spreadsheet component displays a grid. We initialize the action with the default for the Spreadsheet component so that they are synchronized at startup. Then we connect the Show Grid's toggled(bool) signal to Spreadsheet component's setShowGrid(bool) slot, which it inherits from QTableWidget. Once this action is added to a menu or toolbar, the user can toggle the grid on and off.

The Show Grid and Auto-Recalculate actions are independent checkable actions. Qt also supports mutually exclusive actions through the QActionGroup class.

```
aboutQtAction = new QAction(tr("About &Qt"), this);
aboutQtAction->setStatusTip(tr("Show the Qt library's About box"));
connect(aboutQtAction, SIGNAL(triggered()), qApp, SLOT(aboutQt())));
```

For the About Qt action, we use the QApplication aboutQt() slot, accessible through the qApp global variable. This pops up the dialog shown in Figure 3.4.

# Figure 3.4. About Qt

# About Qt

![](img/5a524abdf0b0d58fa99d30abb4463611_105_0.png)

Now that we have created the actions, we can move on to building a menu system containing:

```
void MainWindow::createMenus()
{
    fileMenu = menuBar()->addMenu(tr("File"));
    fileMenu->addAction(newAction());
    fileMenu->addAction(openAction());
    fileMenu->addAction(saveAction());
    fileMenu->addAction(saveAsAction());
    separatorAction = fileMenu->addSeparator();
    for (int i = 0; i < MaxRecentFiles; ++i)
        fileMenu->addAction(recentFileActions[i]);
    fileMenu->addSeparator();
    fileMenu->addAction(exitAction());
```

In Qt, menus are instances of QMenu. The addMenu() function creates a QMenu with the specified text and adds it to the menu bar. QMainWindow::menuBar() returns a pointer to a QMenuBar. The menu bar is created the first time menuBar() is called.

We start by creating the File menu and then the New, Open, Save, and Save As actions to it. We insert a separator to visually group related items. We use a loop to add the (initially hidden) actions from the recentFileActions array, and then add the exitAction at the end.

We have kept a pointer to one of the separators. This will allow us to hide the separator (if there are no recent files) or to show it, since we do not want to show two separators with nothing in between.

```
editMenu = menuBar()->addMenu(tr("\\&Edit"));
```

```
editMenu->addAction(cutAction);
editMenu->addAction(copyAction);
editMenu->addAction(pasteAction);
editMenu->addAction(deleteAction);
```

```
selectSubMenu = editMenu->addMenu(tr("Select"));
selectSubMenu->addAction(rowAction);
selectSubMenu->addAction(columnAction);
selectSubMenu->addAction(selectAllAction);
```

```
editMenu->addSeparator();
editMenu->addAction(findAction);
editMenu->addAction(gotoAction);
```

We create the Edit menu, adding actions with QMenu for the File menu, adding the submenu where we want it. To add the submenu, like the menu it belongs to, we create the

```
toolsMenu = menuBar()->addMenu(tr("Tools"));
toolsMenu->addAction(calculateAction);
toolsMenu->addAction(sortAction);
```

```
optionsMenu = menuBar()->addMenu(tr("Options"));
optionsMenu->addAction(gridAction);
optionsMenu->addAction(recalcAction);
```

```
menuBar()->addSeparator();
```

```
helpMenu = menuBar()->addMenu(tr("Help"));
helpMenu->addAction(aboutAction);
helpMenu->addAction(exit);
```

We create the Tools, Options, and Help menus in a similar fashion. We insert a separator between the Options and Help. In Motif styles, the separator pushes the Help menu to the right; in other styles, the separator is ignored. Figure 3.5 shows both cases.

# Figure 3.5. The menu bar in Motif styles

| File | Edit | Tools | Help |
| :--- | :--- | :--- | :--- |

```
MainWindow::createContextMenu()
{
  spreadsheet->addAction(cutAction);
  spreadsheet->addAction(copyAction);
  spreadsheet->addAction(pasteAction);
  spreadsheet->setContextMenuPolicy(Qt::Actions);
}
```

Any widget has a list of Actions associated with it. To provide context menus for the Spreadsheet, we add the desired actions, create a QMenu and populate it with actions. Figure 3.6 shows the.

# Figure 3.6. The Spreadsheet's context menu

![](img/5a524abdf0b0d58fa99d30abb4463611_107_0.png)

A more sophisticated way of providing context menus is to reimplement the Widget::contextMenuEvent() function.

```
void MainWindow::createToolBars()
{
  fileBar = addToolbar(tr("File"));
  fileBar->addAction(newAction());
  fileBar->addAction(openAction());
  fileBar->addAction(saveAction());

  editToolBar = addToolbar(tr("Edit"));
  editToolBar->addAction(cutAction);
  editToolBar->addAction(copyAction);
  editToolBar->addAction(pasteAction);
  editToolBar->addSeparator();
  editToolBar->addAction(findAction);
  editToolBar->addAction(gotoAction);
}
```

Creating toolbars is very similar to creating menus. We create a File and Edit toolbar. Just like a menu, a toolbar can have separators, as Figure 3.7

# Figure 3.7. The Spreadsheet's toolbars

![](img/5a524abdf0b0d58fa99d30abb4463611_108_0.png)

# Setting Up the Status Bar

With the menus and toolbars complete, we are ready to tackle the Spreadsheet's status bar. In its normal state, the status bar contains two indicators: the current cell's location and the current cell's formula. The status bar is also used to display status tips and other temporary messages. Figure 3.8 shows the status bar in each cell.

```
void MainWindow::createStatusBar()
{
  locationLabel = new QLabel("W999 ");
  locationLabel->setAlignment(Qt::AlignCenter);
  locationLabel->setMinimumSize(locationLabel->sizeHint());

  formulaLabel = new QLineEdit();
  formulaLabel->setWidget(3);

  statusBar()->addWidget(locationLabel);
  statusBar()->addWidget(formulaLabel, 1);

  connect(spreadsheet, SIGNAL(currentCellChanged(int, int, int, int)),
         this, SLOT(updateStatusBar()));
  connect(spreadsheet, SIGNAL(modified()),
         this, SLOT(spreadsheetModified()));
  updateStatusBar();
}
```

The MainWindow::statusBar() function returns a pointer to the status bar. The status bar is created the first time statusBar() is called.) The status indicators are simply QLabels whose text we change whenever necessary. We have added an indent to the formulaLabel so that the text shown in is offset slightly from the left edge. When the QLabels are added to the status bar, they are automatically remapped to make them children of the status bar.

# ### Figure 3.8. The Spreadsheet's status bar

![](img/5a524abdf0b0d58fa99d30abb4463611_109_0.png)

The cell
