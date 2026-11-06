```
```cpp
operator>>(cin, phone2);
```
```

![](bbox=[0.12, 0.222, 0.19, 0.276])

# Good Programming Practice 10.1

*Overloaded operators should mimic the functionality of their built-in counterparts—e.g., the `+` operator should perform addition, not subtraction. Avoid excessive or inconsistent use of operator overloading, as this can make a program cryptic and difficult to read.*

# Overloading the Stream Insertion (`<<`) Operator

The stream insertion operator function (**Fig. 10.4**, lines 10–16) takes an `ostream` reference (`output`) and a `const PhoneNumber` reference (`number`) as arguments and returns an `ostream` reference. Function `operator<<` displays objects of type `PhoneNumber`. When the compiler sees the expression

```
```cpp
cout << phone
```
```