```
dispShftCmd,
const string& shftCmd);
};
```

Of course, this function will also need to lay out the buttons based on some suitable algorithm. My trivial algorithm simply places buttons left to right with four buttons in a row.

As was briefly mentioned in Chapter 6, the MainWindow class also includes a setupFinalButtons() function and a fixSize() function. The setupFinalButtons() function adds the undo, redo, and proc (see Chapter 8) buttons as the top row in the GUI. The fixSize() function forces the GUI’s geometry to stay fixed at its current dimensions. These operations can only logically be called after all plugin buttons have been added.

Unlike the registerCommand() function of the CommandRegistry, the addCommandButton() was not a preexisting public function of the MainWindow class.