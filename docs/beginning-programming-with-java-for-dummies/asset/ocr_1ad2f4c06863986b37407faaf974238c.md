```
```java
lastName = "" +
    (char) (myRandom.nextInt(26) + 'A') +
    (char) (myRandom.nextInt(26) + 'a') +
    (char) (myRandom.nextInt(26) + 'a');

id = myRandom.nextInt(10000);
balance = myRandom.nextInt(10000);
}

void display() {
    NumberFormat currency =
        NumberFormat.getCurrencyInstance();

    out.print("The account with last name ");
    out.print(lastName);
    out.print(" and ID number ");
    out.print(id);
    out.print(" has balance ");
    out.println(currency.format(balance));
}
}
```
```

I wrote some code to use the class in Listing 19-4. This new code is in Listing 19-5.

# Listing 19-5: This Is So Cool!

```
```java
class ProcessBetterAccounts {

    public static void main(String args[]) {

        BetterAccount anAccount;

        for (int i = 0; i < 3; i++) {
            anAccount = new BetterAccount();
            anAccount.fillWithData();
            anAccount.display();
        }
    }
}
```
```

Listing 19-5 is pretty slick. Because the code in Listing 19-4 is so darn smart, the new code in Listing 19-5 has very little work to do. This new code just creates a BetterAccount object and then calls the methods in Listing 19-4. When you run all this stuff, you get results like the ones in Figure 19-3.