KeyChar contains the char equivalent of the character that was pressed. Key contains a value from the ConsoleKey enumeration, which is an enumeration of all the keys on the keyboard. Modifiers describes which, if any, of the keyboard modifiers ALT, CTRL, or SHIFT were pressed when the keystroke was generated. These modifiers are represented by the ConsoleModifiers enumeration, which has these values: Control, Shift, and Alt. More than one modifier value might be present in Modifiers.

The major advantage to ReadKey() is that it provides a means of achieving interactive keyboard input because it is not line buffered. To see the effect of this, try the following program:

```
```
// Read keystrokes from the console by using ReadKey().

using System;

class ReadKeys {
    static void Main() {
        ConsoleKeyInfo keypress;

        Console.WriteLine("Enter keystrokes. Enter Q to stop.");

        do {
            keypress = Console.ReadKey(); // read keystrokes

            Console.WriteLine(" Your key is: " + keypress.KeyChar);

            // Check for modifier keys.
            if((ConsoleModifiers.Alt & keypress.Modifiers) != 0)
                Console.WriteLine("Alt key pressed.");
            if((ConsoleModifiers.Control & keypress.Modifiers) != 0)
                Console.WriteLine("Control key pressed.");
            if((ConsoleModifiers.Shift & keypress.Modifiers) != 0)
                Console.WriteLine("Shift key pressed.");
        } while(keypress.KeyChar != 'Q');
    }
}
```
```

A sample run is shown here:

```
```
Enter keystrokes. Enter Q to stop.
a Your key is: a
b Your key is: b
d Your key is: d
A Your key is: A
Shift key pressed.
B Your key is: B
Shift key pressed.
C Your key is: C
Shift key pressed.
• Your key is: •
Control key pressed.
Q Your key is: Q
Shift key pressed.
```
```