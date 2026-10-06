saveState() functions that we used in our Application class.

```
TicToe::TicToe(QWidget *parent)
: QWidget(parent)
{
    clearBoard();
    if (qApp->isSessionRestored()) {
        restoreState();
    }
    setWindowTitle(tr("Tic-Tac-Toe"));
}
```

In the constructor, we clear the board, and if the application was invoked with the -session option, we call the private function restoreState() to reload the old session.

```
void TicToe::clearBoard()
{
    for (int row = 0; row < 3; ++row) {
        for (int column = 0; column < 3; ++column) {
            board[row][column] = Empty;
        }
    }
    turnNumber = 0;
}
```

In clearBoard(), we clear all the cells and set turnNumber to 0.

```
QString TicToe::saveState() const {
    QFile file(sessionFileName());
    if (file.open(QIODevice::WriteOnly)) {
        QTextStream out(&file);
        for (int row = 0; row < 3; ++row) {
            for (int column = 0; column < 3; ++column)
                out << board[row][column];
        }
    }
    return file.fileName();
}
```

In saveState(), we write the state of the board to disk. The format is straightforward, with 'X' for crosses, 'O' for noughts, and '-' for empty cells.