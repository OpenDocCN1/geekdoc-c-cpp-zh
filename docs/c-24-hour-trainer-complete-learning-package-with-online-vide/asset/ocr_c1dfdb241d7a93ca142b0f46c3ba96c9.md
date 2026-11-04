```
```
{
    // A method variable.
    int count = 2;
    MessageBox.Show(count.ToString());
}
```
```

In this example, the method-level variable hides the class-level variable with the same name. For example, within the `clickMeButton_Click` event handler, its local version of count is visible and has the value 1. The class-level field with value 0 is hidden.

> > **NOTE** You can still get the class-level value if you prefix the variable with the *executing object*. Recall that the special keyword **this** means "the object that is currently executing this code." That means you could access the class-level field while inside the `clickMeButton_Click` event handler like this:
> >
> > ```
> > private void clickMeButton_Click(object sender, EventArgs e)
> > {
> >     // A method variable.
> >     int count = 1;
> >     MessageBox.Show(count.ToString());
> >     MessageBox.Show(this.count.ToString());
> > }
> > ```
> >
> > Usually it's better to avoid potential confusion by giving the variables different names in the first place.

# Method Variable Lifetime

A variable with method scope is created when its method is executed. Each time the method is called, a new version of the variable is created. When the method exits, the variable is destroyed. If its value is referenced by some other variable, it might still exist, but this variable is no longer available to manipulate it.

One consequence of this is that the variable's value resets each time the method executes. For example, consider the following code:

```
```
private void clickMeButton_Click(object sender, EventArgs e)
{
    // A method variable.
    int count = 0;
    count++;
    MessageBox.Show(count.ToString());
}
```
```

Each time this code executes, it creates a variable named count, adds 1 to it, and displays its value. The intent may be to have the message box display an incrementing counter but the result is actually the value 1 each time the user clicks the button.