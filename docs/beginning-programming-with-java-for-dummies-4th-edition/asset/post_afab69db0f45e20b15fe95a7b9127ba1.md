
Figure 7-10 shows a close-up view of the postincrement operator's action. In Figure 7-10, the computer encounters the System.out.println(gumballs++) statement. First, the computer executes System.out.println, using the old value of gumballs (28). Then the computer adds 1 to gumballs (raising the value of gumballs to 29).

### Figure 7-10: The postincrement operator in action.

![](img/bf4858233d2b2a32ff4e3991860526b3_161_0.png)

Look at the bold line of code in Figure 7-11. The computer prints the old value of gumballs (28) on the screen. Only after printing this old value does the computer add 1 to gumballs (raising the gumballs value from 28 to 29).

### Figure 7-11: Using postincrement.

![](img/bf4858233d2b2a32ff4e3991860526b3_161_1.png)

```
class AddEvenMoreGumballs {
    public static void main(String args[]) {
        int gumballs = 27;
        gumballs++;
        System.out.println(gumballs);
        System.out.println(gumballs++);
        System.out.println(gumballs);
    }
}
```

### REMEMBER

With System.out.println(gumballs++), the computer adds 1 to gumballs after printing the old value that gumballs already had.

A run of the code in Figure 7-11 is shown in Figure 7-12. Compare Figure 7-12 with the run in Figure 7-8.

Figure 7-12: A run of the postincrement code (the code in Figure 7-11).

![](img/bf4858233d2b2a32ff4e3991860526b3_162_0.png)

- With preincrement in Figure 7-8, the second number that's displayed is 29.
- With postincrement in Figure 7-12, the second number that's displayed is 28.

In Figure 7-12, the number 29 doesn't show up on the screen until the end of the run, when the computer executes one last System.out.println(gumballs).

![](img/bf4858233d2b2a32ff4e3991860526b3_162_1.png)

Are you trying to decide between using preincrement or postincrement? Ponder no longer. Most programmers use postincrement. In a typical Java program, you often see things like gumballs++. You seldom see things like ++gumballs.

In addition to preincrement and postincrement, Java has two operators that use --. These operators are called predecrement and postdecrement.

- With predecrement (--gumballs), the computer subtracts 1 from the variable's value before the variable is used in the rest of the statement.
- With postdecrement (gumballs--), the computer subtracts 1 from the variable's value after the variable is used in the rest of the statement.

## Assignment operators

If you read the previous section — the section about operators that add 1 — you may be wondering whether you can manipulate these operators to add 2, or add 5, or add 100000. Can you write gumballs+++ and still call yourself a Java programmer? Well, you can't. If you try it, Eclipse will give you an error message:

```
Invalid argument to operation ++/--
```

### Statements and expressions

Any part of a computer program that has a value is called an expression. If you write

```
gumballs = 30;
```

then 30 is an expression (an expression whose value is the quantity 30). If you write

```
amount = 5.95 + 25.00;
```

then 5.95 + 25.00 is an expression (because 5.95 + 25.00 has the value 30.95). If you write

```
gumballsPerKid =
    gumballs / kids;
```

then gumballs / kids is an expression. (The value of the expression gumballs / kids depends on whatever values the variables gumballs and kids have when the expression is executed.)

This brings us to the subject of the pre- and postincrement and decrement operators. There are two ways to think about these operators: the way everyone understands it and the right way. The way I explain it in most of this section (in terms of time, with before and after) is the way everyone understands the concept. Unfortunately, the way everyone understands the concept isn't really the right way. When you see ++ or --, you can think in terms of time sequence. But occasionally some programmer uses ++ or -- in a convoluted way, and the notions of before and after break down. So if you're ever in a tight spot, you should think about these operators in terms of statements and expressions.

First, remember that a statement tells the computer to do something, and an expression has a value. (Statements are described in Chapter 4, and expressions are described earlier in this sidebar.) Which category does gumballs++ belong to? The surprising answer is both. The Java code gumballs++ is both a statement and an expression.

Suppose that, before executing the code System.out.println(gumballs++), the value of gumballs is 28:

- As a statement, gumballs++ tells the computer to add 1 to gumballs.
- As an expression, the value of gumballs++ is 28, not 29.

So even though gumballs gets 1 added to it, the code System.out.println(gumballs++) really means System.out.println(28). (See the figure in this sidebar.)

![](img/bf4858233d2b2a32ff4e3991860526b3_164_0.png)

Now, almost everything you just read about gumballs++ is true about ++gumballs. The only difference is, as an expression, ++gumballs behaves in a more intuitive way. Suppose that before executing the code System.out.println(++gumballs), the value of gumballs is 28:

- As a statement, ++gumballs tells the computer to add 1 to gumballs.
- As an expression, the value of ++gumballs is 29.

So with System.out.println(++gumballs), the variable gumballs gets 1 added to it, and the code System.out.println(++gumballs) really means System.out.println(29).

If you don't use Eclipse, you may see a different error message:

```
unexpected type
required: variable
found   : value
gumballs^+++;
```

Eclipse or no Eclipse, the bottom line is the same: namely, your code contains an error, and you have to fix it.

So how can you add values other than 1? As luck would have it, Java has plenty of assignment operators you can use. With an assignment operator, you can add, subtract, multiply, or divide by anything you want. You can do other cool operations, too.

For example, you can add 1 to the kids variable by writing

```
kids += 1;
```

Is this better than kids++ or kids = kids + 1? No, it's not better. It's just an alternative. But you can add 5 to the kids variable by writing

```
kids += 5;
```

You can't easily add 5 with preincrement or postincrement. And what if the kids get stuck in an evil scientist's cloning machine? The statement

```
kids *= 2;
```

multiplies the number of kids by 2.

With the assignment operators, you can add, subtract, multiply, or divide a variable by any number. The number doesn't have to be a literal. You can use a number-valued expression on the right side of the equal sign:

```
double amount = 5.95;
double shippingAndHandling = 25.00, discount = 0.15;
amount += shippingAndHandling;
amount -= discount * 2;
```

The preceding code adds 25.00 (shippingAndHandling) to the value of amount. Then the code subtracts 0.30 (discount * 2) from the value of amount. How generous!

If the word "literal" doesn't ring any bells for you, refer to Chapter 4.

![](img/bf4858233d2b2a32ff4e3991860526b3_165_0.png)

### Size Matters

Here are today's new vocabulary words:

- **foregift** (fore-gift) n. A premium that a lessee pays to the lessor upon the taking of a lease.
- **hereinbefore** (here-in-be-fore) adv. In a previous part of this document.

Now imagine yourself scanning some compressed text. In this text, all blanks have been removed to conserve storage space. You come upon the following sequence of letters:

`hereinbeforegiftedit`

The question is, what do these letters mean? If you knew each word's length, you could answer the question.

- here in be foregift edit
- hereinbefore gifted it
- herein before gift Ed it

A computer faces the same kind of problem. When a computer stores several numbers in memory or on a disk, the computer doesn't put blank spaces between the numbers. So imagine that a small chunk of the computer's memory looks like the stuff in Figure 7-13. (The computer works exclusively with zeros and ones, but Figure 7-13 uses ordinary digits. With ordinary digits, it's easier to see what's going on.)

![](img/bf4858233d2b2a32ff4e3991860526b3_166_0.png)

What number or numbers are stored in Figure 7-13? Is it two numbers, 42 and 21? Or is it one number, 4,221? And what about storing four numbers, 4, 2, 2, and 1? It all depends on the amount of space each number consumes.

Imagine a variable that stores the number of paydays in a month. This number never gets bigger than 31. You can represent this small number with just eight zeros and ones. But what about a variable that counts stars in the universe? That number could easily be more than a trillion, and to represent one trillion accurately, you need 64 zeros and ones.

At this point, Java comes to the rescue. Java has four types of whole numbers. Just as in Listing 7-1, I declare

```
int gumballsPerKid;
```

I can also declare

```
byte paydaysInAMonth;
short sickDaysDuringYourEmployment;
long numberOfStars;
```

Each of these types (byte, short, int, and long) has its own range of possible values (see Table 7-1).

| Type Name | Range of Values |
|---|---|
| **Whole Number Types** | |
| byte | -128 to 127 |
| short | -32768 to 32767 |
| int | -2147483648 to 2147483647 |
| long | -9223372036854775808 to 9223372036854775807 |
| **Decimal Number Types** | |
| float | -3.4×10³⁸ to 3.4×10³⁸ |
| double | -1.8×10³⁰⁸ to 1.8×10³⁰⁸ |
