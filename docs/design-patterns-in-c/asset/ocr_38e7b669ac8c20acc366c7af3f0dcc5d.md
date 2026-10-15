```
command = new RectangleCommand(_bitmap, _activeColor, e.X, e.Y);
command.Do();
_commandStack.Push(command);
RefreshUI();
}
```

Let us take an example: assume the user clicked the mouse at Point X=100 and Y=200. As the _activeShape is Square, a new SquareCommand class instance is created with arguments e.X and e.Y. The remaining arguments are bitmap and the active color. Then the command instance would be pushed to a stack and the Do() operation is called.

The stack provides a storage for usage of the command instance later. The declaration of stack is:

```
private Stack<ICommand> _commandStack = new Stack<ICommand>();
```

# Inside the SquareCommand Class

We can have a look on the Square class. Both the SquareCommand and RectangleCommand class will be having same implementations except in the Do() operation of drawing the respective shape.

```
public class SquareCommand : ICommand
{
    private Point _point;
    private Bitmap _bitmap;
    private Graphics _graphics;
    private Color _color;
    public SquareCommand(Bitmap bitmap, Color color, int x, int y)
    {
        _bitmap = bitmap;
        _graphics = Graphics.FromImage(_bitmap);
        _color = color;
        _point = new Point(x, y);
    }

    public void Do()
    {
        // Save the current pixel colors for a future UNDO perform
        SaveCurrentPixels();
        // Do the drawing
        _graphics.FillRectangle(new SolidBrush(_color),
            new Rectangle(_point.X, _point.Y, Width, Height));
    }
    private const int Width = 50;
    private const int Height = 50;
```