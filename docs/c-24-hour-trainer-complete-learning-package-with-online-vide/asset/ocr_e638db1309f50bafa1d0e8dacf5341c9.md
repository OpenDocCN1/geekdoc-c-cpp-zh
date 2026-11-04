```
private void SayClicked()
{
    MessageBox.Show("Clicked");
}
```

When the program starts, the following Load event handler sets the variables method1, method2, and method3 so they point to these two methods. Notice that the code makes method1 and method3 point to the same method, SayHi:

```
// Initialize the delegate variables.
private void Form1_Load(object sender, EventArgs e)
{
    method1 = SayHi;
    method2 = SayClicked;
    method3 = SayHi;
}
```

At this point, the program has defined the delegate type, created three variables of that type, and initialized those variables so they refer to the SayHi and SayClicked methods. Now the program is ready to use the variables.

The program displays three buttons. When you click them, the following event handlers execute. Each button simply invokes the method referred to by one of the delegate variables.

```
// Invoke the method stored in the delegates.
private void method1Button_Click(object sender, EventArgs e)
{
    method1();
}
private void method2Button_Click(object sender, EventArgs e)
{
    method2();
}
private void method3Button_Click(object sender, EventArgs e)
{
    method3();
}
```

When it executes, a Button's event handler doesn't "know" what method is stored in its variable. For example, the last Button invokes method3 without knowing which "real" method will execute.

This isn't an extremely practical program, and it's hard to imagine a situation where you would just want buttons to invoke the methods stored in different delegates. However, this example is much simpler than many programs that use delegates so it's worth studying before you look at more realistic examples.

# Event Handler Delegates

Now that you know a bit about delegates, you can learn how to use them to make an event.

First, in the class that will raise the event, declare a delegate type to define the event handler. Usually developers end the delegate's name with EventHandler to make it obvious what the delegate represents.