![](bbox=[0.17, 0.09, 0.23, 0.14])

The comments in Listing 2-1 give you a complete dialogue of how the code works, so no discussion of it here is needed. Of course, you do want to see the output, which appears in Figure 2-1. The important thing to remember is that rounding is different from truncating in the results that it produces, and each method is appropriate at specific times depending on the rules you want to use. For example, when calculating, in whole dollars, how much someone owes you, you don't want to rely on truncating or you'll end up with less money.

![](bbox=[0.25, 0.3, 0.78, 0.47])

FIGURE 2-1: The formatted output shows the difference between truncating and rounding.

# ## Considering other conversion issues

Another kind of conversion that's useful is converting floating-point numbers (that is, numbers with a decimal point) and integers and vice versa. In C++, this conversion is easy: You just copy one to the other, and C++ takes care of the rest.

The only catch is that when C++ converts from a float to an integer, it always truncates. That is, it doesn't round up: When it converts 5.99 to an integer, it doesn't go up to 6; it goes down to 5. But there's an easy trick around that: Add 0.5 to the number before you convert it. If the number is in the upper half (that is, from 0.5 to 0.9999 and so on), then adding 0.5 first takes the number above or equal to the upper whole number. Then, when the function rounds the number, the number rounds down to the upper whole number. For example, if you start with 4.6, just converting it outputs 4. But if you add 0.5, the 4.6 becomes 5.1, and then when you convert that, you get 5. It works!

Going in the other direction is even easier: To convert an integer to a float, you just copy it. If i is an integer and f is a float, you just set it as follows to convert it:

```
```
f = i;
```
```