# 532 Chapter 10 Objects and Classes

```
<< << "Transaction is aborted.\n"
} else {
    shares += num;
    share_val = price;
    set_tot();
}
```

```
void Stock::sell(long num, double price)
{
    using std::cout;
    if (num < 0) {
        cout << "Number of shares sold can't be negative. "
        cout << "Transaction is aborted.\n";
    }
} else if (num > shares) {
        cout << "You can't sell more than you have! "
        cout << "Transaction is aborted.\n";
    } else {
        shares -= num;
        share_val = price;
        set_tot();
    }
```

```
void Stock::update(double price)
{
    share_val = price;
    set_tot();
}
```

```
void Stock::show()
{
    using std::cout;
    using std::ios_base;
    // set format to:fmtflags or =
    ios_base::setf(ios_base::fixed, ios_base::floatfield);
    std::streamsize prec = cout.precision(3);
}
```

```
cout << "Company: " << company
```