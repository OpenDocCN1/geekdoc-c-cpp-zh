# 3.6.3 `deposit` Member Function
with Validation

Member function `deposit` (lines 20–24) does **not** return any data when it completes its task, so its return type is `void`. The member function receives one `int` parameter named `depositAmount`. Lines 21–23

```
```java
{
    if (depositAmount > 0) { // if the depositAmount is valid
        balance = balance + depositAmount; // add it to the balance
}
```
```

ensure that parameter `depositAmount`’s value is added to the `balance` only if the parameter value is valid (i.e., greater than zero)—another example of validity checking. Line 22 first adds the current `balance` and `depositAmount`, forming a *temporary* sum which is then assigned to `balance`, *replacing* its prior value (recall that addition has a higher precedence than assignment). It’s important to understand that the calculation

```
```java
balance + depositAmount
```
```