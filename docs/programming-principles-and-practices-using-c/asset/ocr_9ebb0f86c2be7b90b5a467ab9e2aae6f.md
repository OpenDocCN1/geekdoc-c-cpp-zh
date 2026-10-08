we decided to let the **kind** of a **Token** be the parentheses and operators themselves. This leads to extremely simple processing of parentheses and operators:

```
```
case '(': case ')': case '+': case '-': case '*': case '/':
    return Token(ch);      // let each character represent itself
```
```

To be honest

# ### 6.8.3 Reading numbers

Now we just have to deal with numbers. That’s actually not that easy. How do we really find the value of `123`? Well, that’s `100+20+3`, but how about `12.34`, and should we accept scientific notation, such as `12.34e5`? We could spend hours or days to get this right, but fortunately, we don’t have to. Input streams know what C++ literals look like and how to turn them into values of type `double`. All we have to do is to figure out how to tell `cin` to do that for us inside `get()`:

```
```
case '1':
case '0': case '1': case '2': case '3': case '4':
case '5': case '6': case '7': case '8': case '9':
{
    cin.putback(ch);             // put digit back into the input stream
    double val;
    cin >> val;                  // read a floating-point number
    return Token('8',val);       // let '8' represent “a number”
}
```
```

We – somewhat arbitrarily – chose `'8'` to represent “a number” in a `Token`.

How do we know that a number is coming? Well, if we guess from experience or look in a C++ reference (e.g., Appendix A), we find that a numeric literal must start with a digit or . (the decimal point). So, we test for that. Next, we want to let `cin` read the number, but we have already read the first character (a digit or dot), so just letting `cin` loose on the rest will give a wrong result. We could try to combine the value of the first character with the value of the “rest” as read by `cin`; for example, if someone typed `123`, we would get `1` and `cin` would read `23` and we’d have to add `100` to `23`. Yuck! And that’s a trivial case. Fortunately (and not by accident), `cin` works much like `Token_stream` in that you can put a character back into it. So instead of doing any messy arithmetic, we just put the initial character back into `cin` and then let `cin` read the whole number.