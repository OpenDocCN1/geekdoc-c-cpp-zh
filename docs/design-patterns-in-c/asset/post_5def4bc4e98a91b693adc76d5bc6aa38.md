
```csharp
command = new SquareCommand(_bitmap, _activeColor, e.X, e.Y);
command.Do();
_commandStack.Push(command);
RefreshUI();
}
```

Let us take an example: assume the user clicked the mouse at Point X=100 and Y=200. As the `_activeShape` is Square, a new `SquareCommand` class instance is created with arguments `e.X` and `e.Y`. The remaining arguments are bitmap and the active color. Then the `Do()` operation is called and the command instance is pushed to a stack.

The stack provides a storage for usage of the command instance later. The declaration of stack is:

```csharp
private Stack<ICommand> _commandStack = new Stack<ICommand>();
```

### Inside the SquareCommand Class

We can have a look at the `SquareCommand` class. Both the `SquareCommand` and `RectangleCommand` classes will have the same implementations except in the `Do()` operation of drawing the respective shape.

```csharp
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

    private List<Color> _colors = new List<Color>();

    private void SaveCurrentPixels()
    {
        for (int i = _point.X; i < _point.X + Width; i++)
            for (int j = _point.Y; j < _point.Y + Height; j++)
                _colors.Add(_bitmap.GetPixel(i, j));
    }

    /// <summary>
    /// Perform Undo by restoring back the pixels to previous colors
    /// </summary>
    public void Undo()
    {
        int ix = 0;
        for (int i = _point.X; i < _point.X + Width; i++)
            for (int j = _point.Y; j < _point.Y + Height; j++)
                _bitmap.SetPixel(i, j, _colors[ix++]);
    }
}
```

The constructor is called with the bitmap, the active color, and the x, y positions, which are then stored into class fields. When the `Do()` method is called, the current pixel colors are saved into the `_colors` list. This would enable us to perform the `Undo()` method later. After that, the `Graphics.FillRectangle()` method is called to draw the square. The width and height of the square would be set to 50 pixels using the constants `Width` and `Height` respectively.

The `Undo()` method just restores the previous pixel values using the `Bitmap.SetPixel` method by iterating through each pixel starting from the x, y position.

### Performing the Undo() on clicking Undo button

As we encapsulated each operation into a class with parameters and logged them into the command stack, it is now easier to call the `Undo()` method. Please note that on clicking the Undo button we have to remove the last operation instance from the stack and call its `Undo()` method.

The code for it is:

```csharp
private void UndoButton_Click(object sender, EventArgs e)
{
    // Check command stack contains items
    if (_commandStack.Count > 0)
    {
        // Remove the last command
        ICommand lastCommand = _commandStack.Pop();
        // Call the Undo method
        lastCommand.Undo();
    }
}
```

## 3. Adapter Pattern

Most of you might have heard about Adapter Pattern. It is a pattern commonly used in our applications but without knowing it. Adapter Pattern is one among the 23 Design Patterns. In this chapter I would like to examine this pattern using a simple example.

### Challenge

You are working on a Square class. You need to find the Area of it using Calculator class. But the Calculator class only takes Rectangle class as input. How to solve this scenario?

| Have | Required |
|---|---|
| ![](img/10a39e9a5b1ae55cb003d638eba7aaa0_14_0.png) | ![](img/10a39e9a5b1ae55cb003d638eba7aaa0_14_1.png) |

### Definition

GoF Definition: "Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces."

### Implementation

Following are the class definitions for Rectangle and Calculator.

```csharp
public class Rectangle
{
    public int Width;
    public int Height;
}

public class Calculator
{
    public int GetArea(Rectangle rectangle)
    {
        int area = rectangle.Width * rectangle.Height;
        return area;
    }
}
```

As we can see from the above example, an instance of Rectangle is needed to calculate the area. If we have a Square class of the definition below, the calculation cannot be done.

```csharp
public class Square
{
    public int Size;
}
```

Here we have to create a new CalculatorAdapter to get the work done.

```csharp
public class CalculatorAdapter
{
    public int GetArea(Square square)
    {
        Calculator calculator = new Calculator();

        Rectangle rectangle = new Rectangle();
        rectangle.Width = rectangle.Height = square.Size;

        int area = calculator.GetArea(rectangle);

        return area;
    }
}
```

The CalculatorAdapter performs the following functions:

- Takes the Square parameter
- Convert Square to Rectangle
- Call the original Calculator.GetArea() method
- Return the value received

The invoking code is shown below:

```csharp
// Create Square class and assign Size from UI
Square square = new Square();
square.Size = SquarePanel.Width;

// Use Adapter to calculate the area
CalculatorAdapter adapter = new CalculatorAdapter();
int area = adapter.GetArea(square);

// Display the result back to UI
ResultLabel.Text = "Area: " + area.ToString();
```

On running the sample application we can see the following results.

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_16_0.png)

### Note

We can have other examples including Interfaces to show the above pattern. For simplicity I have avoided the interfaces. In real life the AC to DC adapter is an example of the Adapter pattern as it makes the incompatible device and power supply work together.

### Summary

In this chapter we have explored Adapter pattern. This pattern is useful in scenarios where incompatible types are dealt with. The associated source code contains the example application we have discussed.

## 4. Decorator Pattern

In this chapter I would like to demonstrate the Decorator Pattern. It provides a new way of adding responsibilities at runtime and thus a good alternative to sub classing.

### Challenge

You have an Album class today which is just blank now. Tomorrow the customer wants a Christmas tree on that. You need to achieve this without modifying the Album class.

How to achieve this during runtime?

### Definition

GoF Definition: "Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to sub classing for extending functionality"

### Closed for Modification and Open for Extension

One of the main challenges we face in development is change. The Closed for Modification and Open for Extension principle says a new functionality can be added by keeping the original code unchanged.

### Example:

We will modify the original Album class to incorporate the Christmas tree on it. This should not be the best approach. There is a better approach to this. We can still keep the Album class unchanged and add the Christmas tree to it. Everything happens at runtime – that is the cool part of it.

### Some more examples

We can see real life controls like Form, Button etc. There would be a Form class with built-in functionality. Still the user can use it and add new controls to it / extend the functionality. Here we will be basically deriving from the existing Form/Button class and add new methods or properties to it.

The difference between the above approach and Decorator pattern is that, in the Decorator pattern, it is done during runtime.

### Conclusion on Change

So basically we can conclude that whenever changes are required, the possible solutions could be:
