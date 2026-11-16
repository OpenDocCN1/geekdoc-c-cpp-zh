# HOW'D YOU DO?

Were you surprised that you knew so much about these two controls?

In C#, write an if statement that displays a MessageBox if the actual height of MyDatePicker is less than the requested height.

```
if (MyDatePicker.ActualHeight < MyDatePicker.Height)
    MessageBox.Show("Didn't get as much as I asked for");
```

In XAML, define a Calendar that displays its text using the Times New Roman FontFamily.

```
<Calendar FontFamily="Times New Roman" />
```

In C#, use a MessageBox to display the Name property of MyCalendar.

```
MessageBox.Show(MyCalendar.Name);
```

In C#, write a function that changes the background color of any control to the Beige static property of the Brushes class.

```
void ChangeBackground(Control ctrl)
{
    ctrl.Background = Brushes.Beige;
}
```

The Brushes class is implemented in System.Windows.Media. It defines the standard colors as static properties. XAML knows what you mean if you just refer to the color name, but in C#, you have to reference the class itself.

In XAML, define a DatePicker that has a Foreground color of AliceBlue.

```
<DatePicker Foreground="AliceBlue" />
```

# ON YOUR OWN

Do you know (or can you guess) what all the members of the classes shown in the diagram represent? If there are any that seem obscure, check them out in MSDN.