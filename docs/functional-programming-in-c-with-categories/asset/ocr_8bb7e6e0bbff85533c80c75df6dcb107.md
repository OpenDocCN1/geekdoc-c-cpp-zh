```
DiscountDelegate discountFunc = GetDiscountedPrice;
```

```
double DiscountDelegate(double price, double discount)
```

> Intellisense information

# C#3.0 lambda expression

After C# 3.0 we do not have to declare delegates anymore, and we instead use the generic Func<>. For example, we can write the following:

```
Func<double, double, double> discountFunc = GetDiscountedPrice
```

The Func<double, double, double> represents a Delegate Type that has the following signature (A, B) → C

![](bbox=[0.15, 0.52, 0.85, 0.7])

And we can assign a lambda expression directly to a Func<...>

```
public delegate TResult Func<in T, out TResult>(T arg);
```

```
public delegate TResult Func<in T1, in T2, out TResult>(T1 arg1, T2 arg2);
```

they are just delegate declarations.

All the following statements are equivalent :

```
Func<double,double,double> getDiscount = (double price,double discount) => { return price-discount * price; };
```

```
Func<double, double, double> getDiscount1 = (double price, double discount) => price-discount * price;
```

```
Func<double, double, double> getDiscount2 = (price, discount) => price-discount * price;
```

hopefully, you are already familiar with this notation, but in case you are not, let us go through each one by one briefly. Firstly, the following is an lambda expression :

```
(double price,double discount) =>{ return price - discount * price; };
```

And is just a function. We can remove the { return __ }; with the resulting expression:

```
Func<double, double, double> getDiscount = (double price, double discount) => price - discount * price;
```

Remove double keyword

```
Func<double, double, double> getDiscount2 = (price, discount) => price-discount * price;
```