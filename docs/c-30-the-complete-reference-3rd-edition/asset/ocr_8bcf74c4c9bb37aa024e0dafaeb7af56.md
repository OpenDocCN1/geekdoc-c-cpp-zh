```
KeyEventArgs k = new KeyEventArgs();

if(KeyPress != null) {
    x.ch = key;
    KeyPress(this, k);
}
}

// Demonstrate KeyEvent.
class KeyEventDemo {
    static void Main() {
        KeyEvent kevt = new KeyEvent();
        ConsoleKeyInfo key;
        int count = 0;

        // Use a lambda expression to display the keypress.
        kevt.KeyPress += (source, arg) =>
            Console.WriteLine(" Received keystroke: " + arg.ch);

        // Use a lambda expression to count keypresses.
        kevt.KeyPress += (source, arg) =>
            count++; // count is an outer variable

        Console.WriteLine("Enter some characters. " +
            "Enter a period to stop.");
        do {
            key = Console.ReadKey();
            kevt.OnKeyPress(key.KeyChar);
        } while(key.KeyChar != '.');
        Console.WriteLine(count + " keys pressed.");
    }
}
```

Here is a sample run:

```
Enter some characters. Enter a period to stop.
t Received keystroke: t
e Received keystroke: e
s Received keystroke: s
t Received keystroke: t
. Received keystroke: .
5 keys pressed.
```

The program begins by deriving a class from EventArgs called KeyEventArgs, which is used to pass a keystroke to an event handler. Next, a delegate called KeyHandler defines the event handler for keypress events. The class KeyEvent encapsulates the keypress event. It defines the event KeyPress.

In Main(), a KeyEvent object called kevt is created. Next, an event handler based on a lambda expression is added to kevt.KeyPress that displays each key as it is entered, as shown here: