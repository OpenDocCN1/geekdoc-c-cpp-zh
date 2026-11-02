**The parentheses contain all the things you're going to pass to the method when you call it.**

When you call a method, you can pass information to that method on the fly. This `display` example, with its empty parentheses, looks strange. That's because no information is passed to the `display` method when you call it. That's okay. I give a meatier example later in this chapter.

# Examining the method's body

The `display` method's body contains some `print` and `println` calls. The interesting thing here is that the body makes reference to the variables `lastName`, `id`, and `balance`. A method's body can do that. But with each object having its own `lastName`, `id`, and `balance` variables, what does a variable in the `display` method's body mean?

Well, when I use the `Account` class, I create little account objects. Maybe I create an object for each row of the table in Figure 19-1. Each object has its own values for the `lastName`, `id`, and `balance` variables, and each object has its own copy of the `display` method.

So take the first `display` method in Figure 19-1 — the method for Aju's account. The `display` method for that object behaves as though it had the code in Listing 19-2.

# Listing 19-2: How the display Method Behaves When No One's Looking

```
/*
* This is not real code:
*/
void display() {
    NumberFormat currency =
        NumberFormat.getCurrencyInstance();

    out.print("The account with last name ");
    out.print("Aju");
    out.print(" and ID number ");
    out.print(9936);
    out.print(" has balance ");
    out.println(currency.format(8734.00));
}
```

In fact, each of the three display methods behaves as though its body has a slightly different code. Figure 19-2 illustrates this idea for two instances of the `Account` class.