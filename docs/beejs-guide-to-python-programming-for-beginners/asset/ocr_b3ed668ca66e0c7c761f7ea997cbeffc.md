To compute the log of a number in Python, use the log() function in the math module. You specify the base as the second argument. (If unspecified, it computes the natural log, base e.)

For example, to compute log₂ 999:

```
import math

print(math.log(999, 2))  # Prints 9.96434086779242

# Because 2^9.96434086779242 == 999. Ish.
```

The big thing to remember there is that as a number gets large, the log of the number remains small. Here are some examples:

| x | log₂x |
|---|------|
| 1 | 0.0000 |
| 10 | 3.3219 |
| 100 | 6.6439 |
| 1000 | 9.9658 |
| 10000 | 13.2877 |
| 100000 | 16.6096 |
| 1000000 | 19.9316 |
| 10000000 | 23.2535 |

The log-base-2 of a big number tends to be a much smaller number.

# 15.12 Rounding

When we round a number, we are looking for the nearest number of a certain number of decimal places, dropping all the decimal places smaller than that.

By default, we mean zero decimal places, i.e. we want to round to the nearest whole number.

So if I said, “Round 2.3 to the nearest whole number,” you’d answer “2”, because that’s the closest whole number to 2.3.

And if I said, “Round 2.8 to the nearest whole number,” you’d answer “3”, because that’s the closest whole number to 2.8.

When we round to a higher number, we call that rounding up.

The other direction is rounding down.

But what if I said “Round 2.5 to the nearest whole number?” It’s perfectly between 2 and 3! In those cases, conventionally, lots of us learned to round up. So the answer would be 3.

We can also force a number to round a certain direction by declaring which way to round.

“Divide x by 3, then round up.”

In Python, we have a few options for rounding.

We can use the built-in round() function.

But it behaves a little bit differently than we might be used to. Notably, numbers like 1.5, 2.5, and 3.5 that are equally close to two whole numbers always round to the nearest even number. This is commonly known as round half to even or banker’s rounding.

```
round(2.8)  # 3
round(-2.2) # -2
round(-2.8) # -3

round(1.5)  # 2
```