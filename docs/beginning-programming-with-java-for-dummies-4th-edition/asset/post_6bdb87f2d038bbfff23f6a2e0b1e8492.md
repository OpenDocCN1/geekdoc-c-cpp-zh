
![](img/bf4858233d2b2a32ff4e3991860526b3_214_0.png)

Figure 10-4: The choices in Listing 10-1.

## More and more conditions

Last night I had a delicious meal at the neighborhood burger joint. As part of a promotion, I got a discount coupon along with the meal. The coupon is good for $2.00 off the price of a ticket at the local movie theater.

To make use of the coupon in the TicketPrice program, I have to tweak the code in Listing 10-1. The revised code is in Listing 10-2. In Figure 10-5, I take that new code around the block a few times.

Figure 10-5: Running the code in Listing 10-2

```text
How old are you? 51
Have a coupon? (Y/N) Y
Please pay $7.25. Enjoy the show!

How old are you? 51
Have a coupon? (Y/N) y
Please pay $7.25. Enjoy the show!

How old are you? 51
Have a coupon? (Y/N) N
Please pay $9.25. Enjoy the show!

How old are you? 51
Have a coupon? (Y/N) Z
Huh?
Please pay $9.25. Enjoy the show!
```

### Listing 10-2: Do You Have a Coupon?

```java
import java.util.Scanner;

class TicketPriceWithDiscount {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;
        char reply;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        System.out.print("Have a coupon? (Y/N) ");
        reply = keyboard.findWithinHorizon(".", 0)
            .charAt(0);

        if (age >= 12 && age < 65) {
            price = 9.25;
        }
        if (age < 12 || age >= 65) {
            price = 5.25;
        }

        if (reply == 'Y' || reply == 'y') {
            price -= 2.00;
        }
        if (reply != 'Y' && reply != 'y' &&
        reply!='N' && reply!='n') {
            System.out.println("Huh?");
        }

        System.out.print("Please pay $");
        System.out.print(price);
        System.out.print(". ");
        System.out.println("Enjoy the show!");
        keyboard.close();
    }
}
```

Listing 10-2 has two if statements whose conditions involve characters:

- In the first such statement, the computer checks to see whether the `reply` variable stores the letter Y or the letter y. If either is the case, it subtracts 2.00 from the `price`. (For information on operators like `-=`, see Chapter 7.)
- The second such statement has a hefty condition. The condition tests to see whether the `reply` variable stores any reasonable value at all. If the reply isn't Y, and isn't y, and isn't N, and isn't n, the computer expresses its concern by displaying, "Huh?" (As a paying customer, the word "Huh?" on the automated ticket teller's screen will certainly get your attention.)

![](img/bf4858233d2b2a32ff4e3991860526b3_216_0.png)

When you create a big multipart condition, you always have several ways to think about the condition. For example, you can rewrite the last condition in Listing 10-2 as if (!(reply == 'Y' || reply == 'y' || reply == 'N' || reply == 'n')). If it's not the case that the reply is either Y, y, N, or n, then display 'Huh?' So which way of writing the condition is better — the way I do it in Listing 10-2, or the way I do it in this tip? It depends on your taste. Whichever makes the logic easier for you to understand is the better way.

## Using boolean variables

No matter how good a program is, you can always make it a little bit better. Take the code in Listing 10-2. Does the forest of if statements make you nervous? Do you slow to a crawl when you read each condition? Wouldn't it be nice if you could glance at a condition and make sense of it very quickly?

To some extent, you can. If you're willing to create some additional variables, you can make your code easier to read. Listing 10-3 shows you how.

### Listing 10-3: George Boole Would Be Proud

```java
import java.util.Scanner;

class NicePrice {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;
        char reply;
        boolean isKid, isSenior, hasCoupon, hasNoCoupon;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        System.out.print("Have a coupon? (Y/N) ");
        reply = keyboard.findWithinHorizon(".", 0)
                .charAt(0);

        isKid = age < 12;
        isSenior = age >= 65;
        hasCoupon = reply == 'Y' || reply == 'y';
        hasNoCoupon = reply == 'N' || reply == 'n';

        if (!isKid && !isSenior) {
            price = 9.25;
        }
        if (isKid || isSenior) {
            price = 5.25;
        }

        if (hasCoupon) {
            price -= 2.00;
        }
        if (!hasCoupon && !hasNoCoupon) {
            System.out.println("Huh?");
        }

        System.out.print("Please pay $");
        System.out.print(price);
        System.out.print(". ");
        System.out.println("Enjoy the show!");

        keyboard.close();
    }
}
```

Runs of the Listing 10-3 code look like the stuff in Figure 10-5. The only difference between Listings 10-2 and 10-3 is the use of boolean variables. In Listing 10-3, you get past all the less-than signs and double equal signs before the start of any if statements. By the time you encounter the two if statements, the conditions can use simple words — words like isKid, isSenior, and hasCoupon. With all these boolean variables, expressing each if statement's condition is a snap. You can read more about boolean variables in Chapter 8.

Adding a boolean variable can make your code more manageable. But some programming languages don't have boolean variables, so many programmers prefer to create if conditions on the fly. That's why I mix the two techniques (conditions with and without boolean variables) in this book.

## Mixing different logical operators together

If you read about Listing 10-2, you know that my local movie theater offers discount coupons. The trouble is, I can't use a coupon along with any other discount. I tried to convince the ticket taker that I'm under 12 years of age, but he didn't buy it. When that didn't work, I tried combining the coupon with the senior citizen discount. That didn't work, either.

The theater must use some software that checks for people like me. It looks something like the code in Listing 10-4. To watch the code run, take a look at Figure 10-6.

Figure 10-6: Running the code in Listing 10-4.

```text
How old are you? 7
Have a coupon? (Y/N) Y
Please pay $5.25. Enjoy the show!

How old are you? 25
Have a coupon? (Y/N) y
Please pay $7.25. Enjoy the show!

How old are you? 25
Have a coupon? (Y/N) n
Please pay $9.25. Enjoy the show!

How old are you? 85
Have a coupon? (Y/N) y
Please pay $5.25. Enjoy the show!

How old are you? 85
Have a coupon? (Y/N) Y
Please pay $5.25. Enjoy the show!
```

### Listing 10-4: No Extra Break for Kids or Seniors

```java
import java.util.Scanner;

class CheckAgeForDiscount {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int age;
        double price = 0.00;
        char reply;

        System.out.print("How old are you? ");
        age = keyboard.nextInt();

        System.out.print("Have a coupon? (Y/N) ");
        reply = keyboard.findWithinHorizon(".", 0)
            .charAt(0);

        if (age >= 12 && age < 65) {
            price = 9.25;
        }
        if (age < 12 || age >= 65) {
            price = 5.25;
        }

        if ((reply == 'Y' || reply == 'y') &&
            (age >= 12 && age < 65)) {
            price -= 2.00;
        }

        System.out.print("Please pay $");
        System.out.print(price);
        System.out.print(".");
        System.out.println("Enjoy the show!");

        keyboard.close();
    }
}
```

Listing 10-4 is a lot like its predecessors, Listings 10-1 and 10-2. The big difference is the bolded if statement. This if statement tests two things, and each thing has two parts of its own:

- ✓ **Does the customer have a coupon?**
  That is, did the customer reply with either Y or y?
- ✓ **Is the customer in the regular age group?**
  That is, is the customer at least 12 years old and younger than 65?
