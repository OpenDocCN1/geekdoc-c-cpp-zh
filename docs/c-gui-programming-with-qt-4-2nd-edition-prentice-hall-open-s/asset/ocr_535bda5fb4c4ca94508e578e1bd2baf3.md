Now let's look at the TicTacoe class:

Code View:

```
class TicTacoe : public QWidget
{
    Q_OBJECT

public:
    TicTacoe(QWidget parent = 0);

    bool gameInProgress() const;
    QString saveState() const;
    QSize sizeHint() const;

protected:
    void paintEvent(QPaintEvent event);
    void mousePressEvent(MouseEvent *event);

private:
    enum { Empty = '-', Cross = 'X', Nought = '0' };

    void clearBoard();
    void restoreState();
    QString sessionFileName() const;
    QRect cellRect(int row, int column) const;
    int cellWidth() const { return width() 3; }
    int cellHeight() const { return height() 3; }
    bool threeInARow(int row1, int col1, int row3, int col3) const;
    char board[3][3];
    int turnNumber();
};
```

The TicTacoe class is derived from QWidget and reimplements sizeHint(), paintEvent(), and mousePressEvent(). It also provides the gameInProgress() *