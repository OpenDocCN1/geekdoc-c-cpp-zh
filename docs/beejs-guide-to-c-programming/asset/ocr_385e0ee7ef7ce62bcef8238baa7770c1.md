# 37.4 Limits of Fixed Size Integers

We also have limits defined so you can get the maximum and minimum values for these types:

```
INT8_MAX INT8_MIN UINT8_MAX
INT16_MAX INT16_MIN UINT16_MAX
INT32_MAX INT32_MIN UINT32_MAX
INT64_MAX INT64_MIN UINT64_MAX
```

```
INT_LEAST8_MAX INT_LEAST8_MIN UINT_LEAST8_MAX
INT_LEAST16_MAX INT_LEAST16_MIN UINT_LEAST16_MAX
INT_LEAST32_MAX INT_LEAST32_MIN UINT_LEAST32_MAX
INT_LEAST64_MAX INT_LEAST64_MIN UINT_LEAST64_MAX
```

```
FAST_8_MAX FAST_8_MIN FAST_8_MAX
FAST_16_MAX FAST_16_MIN FAST_16_MAX
FAST_32_MAX FAST_32_MIN FAST_32_MAX
FAST_64_MAX FAST_64_MIN FAST_64_MAX
```

```
INTMAX_MAX INTMAX_MIN UINTMAX_MAX
```

Note the for all unsigned types it is 0, so, there's no macro for it.

# 37.5 Format Specifiers

In order to print these types, you need to send the right specifier to printf(). (And the same for getting input with scan())

But how are you know what size types are under the hood? Luckily, once again, C provides some macros to help with this.

All this can be found in <inttypes.h>.

Now, we have a bunch of macros. Like a complexity explosion of macros. I'm going to stop listing out every one and just put the lowercase n in the place where you should put 8, 16, 32, or 64 depending on your needs.

Let's look at the macros for printing signed integers:

```
PRId PRIDEASTN PRIdMAX
PRIn PRIDEASTN PRInMAX
```

Look at the patterns. You can see there variants for the fixed, least, and max types.

And you also have a lowercase d and a uppercase i. Those correspond to the printf() format specifiers %d and %i.

So if I have something of:

```
int_least16_t x = 3498;
```

I can print that with the equivalent format specifier for %d by using PRIdLeast16.

But how? How do we use that macro?

First of all, that macro specifies a string containing the letter or letters printf() needs to use to print that type. Like, for example, it could be "d" or "ld"

So we need to be embedded in our format string to the printf() call.