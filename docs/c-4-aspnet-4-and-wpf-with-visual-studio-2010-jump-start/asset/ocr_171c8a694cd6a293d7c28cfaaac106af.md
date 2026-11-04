```
}

// Display a sample of the color.
private void ShowSample()
{
    if (borSample == null) return;

    byte r, g, b;
    try {
        r = byte.Parse(txtRed.Text);
    } catch {
        r = 0;
    }
    try {
        g = byte.Parse(txtGreen.Text);
    } catch {
        g = 0;
    }
    try {
        b = byte.Parse(txtBlue.Text);
    } catch {
        b = 0;
    }
    borSample.Background = new SolidColorBrush(Color.FromRgb(r, g, b));
}
```

> *WPF Programmer's Reference 9780470477229 EventNameAttributes*

# ## RESOURCES

One of the most important concepts in any kind of programming is code reuse. Subroutines, functions, scripts, classes, inheritance, loops, and many other programming constructs let you reuse code in one way or another. For example, if your program needs to perform the same task in many places, you can create a subroutine that performs the task and then call it from those places.

Just as routines and functions let you reuse code in languages such as C# and Visual Basic, *resources* let you reuse XAML code. They let you define values that you can then use from many places in a XAML file.

# ## Defining Resources

Creating and using a simple resource is fairly easy. (In fact, it's easier to understand from an example than from a description, so, if you have trouble understanding the following explanation, look at the example text and then read the explanation again.)

To define a resource, add a `Resources` property element to an object such as a `Window`, `Grid`, or other container. Inside that element, place the resources that you will want to use later. Each resource is an