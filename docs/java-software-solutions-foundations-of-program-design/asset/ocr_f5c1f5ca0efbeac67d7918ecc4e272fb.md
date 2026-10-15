# LISTING 5.3 continued

```
public class CoinFlip
{
    //------------------------------------------------------------
    // Creates a Coin object, flips it, and prints the results.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        Coin myCoin = new Coin();

        myCoin.flip();

        System.out.println (myCoin);

        if (myCoin.isHeads())
            System.out.println ("You win.");
        else
            System.out.println ("Better luck next time.");
    }
}
```

# OUTPUT

Tails
Better luck next time.

The Coin class is shown in Listing 5.4. It stores two integer constants (HEADS and TAILS) that represent the two possible states of the coin, and an instance variable called face that represents the current state of the coin. The Coin constructor initially flips the coin by calling the flip method, which determines the new state of the coin by randomly choosing a number (either 0 or 1). The isHeads method returns a boolean value based on the current face value of the coin. The toString method uses an if-else statement to determine which character string to return to describe the coin. The toString method is automatically called when the myCoin object is passed to println in the main method.

# Using Block Statements

We may want to do more than one thing as the result of evaluating a boolean condition. In Java, we can replace any single statement with a block statement.