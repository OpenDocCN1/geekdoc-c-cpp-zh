```
}
    bounced = true;
}
else if (X + Diameter > Parent.ActualWidth)
{
    // Hit the right edge.
    double overshoot = (X + Diameter) - Parent.ActualWidth;
    X = Parent.ActualWidth - overshoot - Diameter;
    Vx = -Vx;
    bounced = true;
}
Y += Vy;
if (Y < 0)
{
    // Hit the left edge.
    Y = -Y;
    Vy = -Vy;
    bounced = true;
}
else if (Y + Diameter > Parent.ActualHeight)
{
    // Hit the right edge.
    double overshoot = (Y + Diameter) - Parent.ActualHeight;
    Y = Parent.ActualHeight - overshoot - Diameter;
    Vy = -Vy;
    bounced = true;
}

// Update the Ellipse's position.
Canvas.SetLeft(MyEllipse, X);
Canvas.SetTop(MyEllipse, Y);

    return bounced;
}
}
```

When the window loads, create a DispatcherTimer and give it an event handler that moves the balls.

+   1. Add the XAML code Loaded="Page_Loaded" to the main window's definition.
+   2. Use the following code to prepare the program when the window is loaded:

```
// The movement timer.
private DispatcherTimer MoveTimer;

// Balls.
private const int NumBalls = 10;
private Ball[] Balls = new Ball[NumBalls];

// Used to generate random numbers.
private Random Rand = new Random();

// Create balls and start them moving.
private void Page_Loaded(object sender, RoutedEventArgs e)
{
```