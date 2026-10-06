# 16 1 Introduction

example: if the two adds have the same signs, the sum will have exactly the same sign. Otherwise, we have to subtract the small number from the big number and the result will inherit the sign of the bigger number. Furthermore, it is difficult for computer hardware to implement operations such as borrowing. Because of the shortcomings true code has, people try to find other better representations.

# 2. Ones-complement code

Ones-complement code is rarely used, but it may help us understand the meaning of complement code, so we introduce it here.

The ones-complement code of a positive number is the same as true code.
The ones-complement code of a negative number is like this:
The sign is the same as the one in true code, and all the other bits are reversed
(0 → 1, 1 → 0), for example:

```
X = +1100110 [X]true = 01100110 [X]ones_comp = 0110010
X = -1100110 [X]true = 1110110 [X]one_comp = 1001001
X = +0000000 [X]true = 0000000 [X]one_comp = 0000000
X = -0000000 [X]true = 10000000 [X]one_comp = 1111111
```

Like true code, in ones-complement code we have positive zero and negative zero.
The ones-complement code of a decimal fraction is as follows:

```
X = 0.1011 [X]true = 0.1011 [X]one_comp = 0.1011
X = -0.1011 [X]true = 1.1011 [X]one_comp = 1.0100
```

# 3. Complement code

# a) Modulus

In physics, a modulus is the capacity of a certain measurement. For example, the counter of a clock we daily is reset to zero after it reaches 12 (discarding 12), and thus the modulus of the clock is 12. This is a kind of mod operation in mathematics. For example:
++ uses "%%" as the mod arithmetic operator.

```
14 % 12 = 2
```

If the current time is 6 o'clock your watch shows 8, then how do you adjust the watch? Can you subtract two hours from your watch or add 10 hours, and the result is the same:

```
8 - 2 = 6
```

```
(8 + 10) mod 12 = 6
```

In the modulus system:

```
8 - 2 = (8 + 10) mod 12
```