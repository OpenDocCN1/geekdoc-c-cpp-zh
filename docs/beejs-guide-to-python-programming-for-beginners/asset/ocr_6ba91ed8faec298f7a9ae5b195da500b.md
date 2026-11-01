So the base is also tied into the value that any place in a number represents. Which makes sense, since we have to add a new place when we run out of digits, and if we have digits 0-9, that next place must represent the number of 10s, because that's what comes after 9.

# 18.3 Hexadecimal, Base 16

Hexadecimal, or hex for short, is a really common number base for programmers. And it's an interesting one to look at because, at base 16, it has more digits than base 10. With base 10, we have 0-9. But with base 16, we have 0 through... what?

Since we need more symbols to represent digits in base 16 than then normal arabic numerals we use for 0-9, we've gone ahead and co-opted the first part of the latin alphabet. We have 10 digits in 0-9, and we grabbed 6 more "digits" with A-F to get up to 16 total digits.

That means when counting apples on the table in hex, we count:

0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, 10, 11, 12 ...

(Upper and lower case don't matter when writing numbers in hex.)

Look what happened when we got to F and ran out of digits: we added a new place. What value does that place have?

Since this is base 16, it has to be the 16s place.

TODO

# 18.4 Specifying the Number Base in Python

When you write down a number in your code, you have to tell Python what the base is, or it'll assume you mean decimal (base 10).

For example, if I write

```
x = 10101011
```

Is that binary? I mean, it looks like it!

But it's not! Because we didn't indicate otherwise, Python assumes this is the decimal number ten million one hundred one thousand eleven.

We have some options ## Writing Numbers Down

Throughout all this, it's important to remember that number bases are just other languages for representing the same number. You might write number in code as