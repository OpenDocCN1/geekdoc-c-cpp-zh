The program doesn't have to work this way. If I take Listing 9-4 and change hankees > socks to hankees >= socks then, in case of a tie, the Hankees score comes first.

Suppose that you want a bit more control. When the scores are equal, you want an It's a tie message. To do this, think in terms of a three-pronged fork. You have a prong for a Hankees win, another prong for a Socks win, and a third prong for a tie. You can write this code in several different ways, but one way that makes lots of sense is in Listing 10-6. For three runs of the code in Listing 10-6, see Figure 10-12.

# Listing 10-6: In Case of a Tie...

```
import java.util.Scanner;
import static java.lang.System.out;

class WinLoseOrTie {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int hankees, socks;
        out.print("Hankees and Socks scores?  ");
        hankees = keyboard.nextInt();
        socks = keyboard.nextInt();
        out.println();
        if (hankees > socks) {
            out.println("Hankees win...");
            out.print("Hankees:  ");
            out.println(hankees);
            out.print("Socks:  ");
            out.println(socks);
        } else if (socks > hankees) {
            out.println("Socks win...");
            out.print("Socks:  ");
            out.println(socks);
            out.print("Hankees: ");
            out.println(hankees);
        } else {
            out.println("It's a tie...");
            out.print("Hankees: ");
            out.println(hankees);
            out.print("Socks:  ");
            out.println(socks);
        }
        keyboard.close();
    }
}
```