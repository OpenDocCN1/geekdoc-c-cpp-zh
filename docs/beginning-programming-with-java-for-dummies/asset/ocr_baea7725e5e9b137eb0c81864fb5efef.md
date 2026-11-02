The program then stops the repetition when it finds the @ sign. I take a stab at writing this program. My first attempt doesn't work, but it's a darn good start. It's in Listing 12-3.

# Listing 12-3: Trying to Get a Username from an E-Mail Address

```
```java
/*
 * This code does NOT work, but I'm not discouraged.
 */
import java.util.Scanner;

class FirstAttempt {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        char symbol = ' ';
        while (symbol != '@') {
            symbol = keyboard.findWithinHorizon(".", 0)
                .charAt(0);
            System.out.print(symbol);
        }
        System.out.println();
        keyboard.close();
    }
}
```
```

When you run the code in Listing 12-3, you get the output shown in Figure 12-9. The user types one character after another — the letter J, then c, then h, and so on. At first, the program in Listing 12-3 does nothing. (The computer doesn't send any of the user's input to the program until the user presses Enter.) After the user types a whole e-mail address and presses Enter, the program gets its first character (the J in John).

# Figure 12-9: Oops! Got the @ sign, too.

![](bbox=[0.25, 0.88, 0.52, 0.98])

Unfortunately, the program's output isn't what you expect. Instead of just the username John, you get the username and the @ sign.