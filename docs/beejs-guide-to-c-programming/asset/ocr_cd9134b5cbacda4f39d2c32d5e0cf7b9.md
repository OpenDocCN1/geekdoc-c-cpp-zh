# Chapter 26. Locale and Internationalization

By passing in an empty string """ for your argument, you're telling C, "Hey, figure out the current locale on this system is so I don't have to tell you.

# 26.2 Getting the Monetary Locale Settings

Because moving green pieces of paper around promises to be the key to happiness¹, let's talk about monetary locale. When writing portable code, you know what to type for cash, right? Whether that's "S", "C", "V", or "L".

How can you write code with such instance? Luckily, once you call locale(LC_ALL, ""), you can just look this up with a call to localeconv():

```
struct lconv *x = localeconv();
```

This function returns a pointer to a statically-allocated lconv that has all that juicy information you're looking for.

Here are the fields of struct lconv and their meanings.

First, some conversions. An _p means "positive", and n_ means "negative", and int_ means "international". A lot of these are type char or char*, most (or the strings they point to) are actually treated as integers².

Before we go further, know that CHAR_MAX (from <limits>) is the maximum value that can be in a char. And many of the following characters use that to indicate the value is not available in the locale.

| Field | Description |
| char *mon_decimal_point | Decimal character for money

> ¹This planet has—or had—a problem, which this was: most of the people living on it were unhappy for much of the time. Many solutions were suggested for this, but most of these were largely concerned with the movement of green pieces of paper, which was odd because on the whole its small green pieces of paper that were unhappy." —The Hitchhiker’s Guide to the Galaxy, Douglas Adams

> ²Remember that char is just a byte-sized integer.