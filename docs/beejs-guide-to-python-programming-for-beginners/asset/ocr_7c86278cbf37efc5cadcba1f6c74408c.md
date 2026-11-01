```
print(2.7**100)  # 1.3689147905858927e+43
```

What's that e+43 at the end?

This is what we call scientific notation. It's a shorthand way of writing really large (or small) numbers.

The number above, 1.3689147905858927e+43, is saying this, mathematically:

1.3689147905858927 × 10^43

Now, 10^43 is a big number. So multiplying 1.3689 etc. by it results in a very large number, indeed.

But that's not all. We can use it to represent very small numbers, too.

```
print(3.6/500000000000000000)  # 7.2e-19
```

7.2e-19 means:

7.2 × 10^-19

And 10^-19 is a very small number (very close to 0—remember that 10^-19 = 1/10^19), so multiplying 7.2 by it results in a very small number as well.

Remember this:

+   - If you see e-something at the end, it's a very small number (close to 0).
+   - If you see e+ something at the end, it's a very large number (far from 0).

# 15.11 Logarithms

Hang on, because things are about to get weird.

Well, not too weird, but pretty weird.

Logarithms, or logs for short, are kind of the opposite of exponents.

But not opposite in the same way square roots are opposite.

That's convenient, right?

With logs, we say "log base x of y". For example, "log base 2 of 32", which is written like this:

log₂ 32

What that is asking is "2 to the what power is 32?" Or, in math:

These are both true:

x = log₂ 32
2^x = 32

So what's the answer? Some trial and error might lead you to realize that 2^5 = 32, so therefore:

x = log₂ 32 = 5

There are three common bases that you see for logs, though the base can be any number: 2, 10, and e.

Base 2 is super common in programming. In fact, it's so common that if you ever see someone write log n in a computing context, you should assume they mean log₂ n.

e is the base of the natural logarithm, common in math, and uncommon in computing.

So what are they good for?

A common place you see logarithms in programming is when using Big-O notation to indicate computational complexity.