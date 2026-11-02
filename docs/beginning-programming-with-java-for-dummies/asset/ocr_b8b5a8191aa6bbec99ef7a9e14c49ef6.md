![](bbox=[0.151, 0.116, 0.795, 0.442])

Figure 19-2: Two objects, each with its own display method.

# Calling the method

To put the previous section's ideas into action, you need more code. So the next listing (see Listing 19-3) creates instances of the Account class.

# Listing 19-3: Making Use of the Code in Listing 19-1

```
```java
import java.util.Random;

class ProcessAccounts {

    public static void main(String args[]) {

        Random myRandom = new Random();
        Account anAccount;

        for (int i = 0; i < 3; i++) {
            anAccount = new Account();

            anAccount.lastName = "" +
                    (char) (myRandom.nextInt(26) + 'A') +
                    (char) (myRandom.nextInt(26) + 'a') +
                    (char) (myRandom.nextInt(26) + 'a');

            anAccount.id = myRandom.nextInt(10000);
            anAccount.balance = myRandom.nextInt(10000);
            anAccount.display();
        }
    }
}
```
```