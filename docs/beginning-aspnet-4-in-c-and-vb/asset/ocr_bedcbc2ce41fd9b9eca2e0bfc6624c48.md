```
uint bal = 350;
Currency balance = bal;
uint bal2 = (uint)balance;
```

The answer is not 350 but 3! Moreover, it all follows logically. You convert 350 implicitly to a Currency, giving the result balance.Dollars = 3, balance.Cents = 50. Then the compiler does its usual figuring out of the best path for the conversion back. Balance ends up being implicitly converted to a float (value 3.5), and this is converted explicitly to a uint with value 3.

Of course, other instances exist in which converting to another data type and back again causes data loss. For example, converting a float containing 5.8 to an int and back to a float again will lose the fractional part, giving you a result of 5, but there is a slight difference in principle between losing the fractional part of a number and dividing an integer by more than 100. Currency has suddenly become a rather dangerous class that does strange things to integers!

The problem is that there is a conflict between how your casts interpret integers. The casts between Currency and float interpret an integer value of 1 as corresponding to one dollar, but the latest uint-to-Currency cast interprets this value as one cent. This is an example of very poor design. If you want your classes to be easy to use, you should make sure that all your casts behave in a way that is mutually compatible, in the sense that they intuitively give the same results. In this case, the solution is obviously to rewrite the uint-to-Currency cast so that it interprets an integer value of 1 as one dollar:

```
public static implicit operator Currency (uint value)
{
    return new Currency(value, 0);
}
```

Incidentally, you might wonder whether this new cast is necessary at all. The answer is that it could be useful. Without this cast, the only way for the compiler to carry out a uint-to-Currency conversion would be via a float. Converting directly is a lot more efficient in this case, so having this extra cast provides performance benefits, though you need to make sure it gives the same result as via a float, which you have now done. In other situations, you may also find that separately defining casts for different predefined data types allows more conversions to be implicit rather than explicit, though that is not the case here.

A good test of whether your casts are compatible is to ask whether a conversion will give the same results (other than perhaps a loss of accuracy as in float-to-int conversions), regardless of which path it takes. The Currency class provides a good example of this. Look at this code:

```
Currency balance = new Currency(50, 35);
ulong bal = (ulong) balance;
```

At present, there is only one way that the compiler can achieve this conversion: by converting the Currency to a float implicitly, then to a ulong explicitly. The float-to-ulong conversion requires an explicit conversion, but that is fine because you have specified one here.

Suppose, however, that you then added another cast, to convert implicitly from a Currency to a uint. You will actually do this by modifying the Currency struct by adding the casts both to and from uint. This code is available as the SimpleCurrency2 example:

```
public static implicit operator Currency (uint value)
{
    return new Currency(value, 0);
}

public static implicit operator uint (Currency value)
{
    return value.Dollars;
}
```

Now the compiler has another possible route to convert from Currency to ulong: to convert from Currency to uint implicitly, then to ulong implicitly. Which of these two routes will it take? C# has some precise rules about the best route for the compiler if there are several possibilities. (The rules are not detailed in this