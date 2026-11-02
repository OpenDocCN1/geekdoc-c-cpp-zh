with zeros and ones, but Figure 7-13 uses ordinary digits. With ordinary digits, it's easier to see what's going on.)

![](bbox=[0.12, 0.25, 0.5, 0.35])

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