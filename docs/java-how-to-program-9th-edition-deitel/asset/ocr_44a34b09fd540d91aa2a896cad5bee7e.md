```
// Keypad.java
// Represents the keypad of the ATM
import java.util.Scanner; // program uses Scanner to obtain user input

public class Keypad
{
    private Scanner input; // reads data from the command line

    // no-argument constructor initializes the Scanner
    public Keypad()
    {
        input = new Scanner( System.in );
    } // end no-argument Keypad constructor

    // return an integer value entered by user
    public int getInput()
    {
        return input.nextInt(); // we assume that user enters an integer
    } // end method getInput
} // end class Keypad
```

Fig. 13.15 | Class Keypad represents the ATM’s keypad.

method nextInt (line 18) to return the next integer input by the user. [Note: Method nextInt can throw an InputMismatchException if the user enters non-integer input. Because the real ATM’s keypad permits only integer input, we assume that no exception will occur and do not attempt to fix this problem. See Chapter 11, Exception Handling: A Deeper Look, for information on catching exceptions.] Recall that nextInt obtains all the input used by the ATM. Keypad’s getInput method simply returns the integer input by the user. If a client of class Keypad requires input that satisfies some criteria (i.e., a number corresponding to a valid menu option), the client must perform the error checking.

# 13.4.4 Class CashDispenser

Class CashDispenser (Fig. 13.16) represents the cash dispenser of the ATM. Line 7 declares constant INITIAL_COUNT, which indicates the initial count of bills in the cash dispenser when the ATM starts (i.e., 500). Line 8 implements attribute count (modeled in Fig. 13.10), which keeps track of the number of bills remaining in the CashDispenser at any time. The constructor (lines 11–14) sets count to the initial count. CashDispenser has two public methods—dispenseCash (lines 17–21) and isSufficientCashAvailable (lines 24–32). The class trusts that a client (i.e., Withdrawal) calls dispenseCash only after establishing that sufficient cash is available by calling isSufficientCashAvailable. Thus, dispenseCash simply simulates dispensing the requested amount without checking whether sufficient cash is available.

```
// CashDispenser.java
// Represents the cash dispenser of the ATM
```

Fig. 13.16 | Class CashDispenser represents the ATM’s cash dispenser. (Part 1 of 2.)