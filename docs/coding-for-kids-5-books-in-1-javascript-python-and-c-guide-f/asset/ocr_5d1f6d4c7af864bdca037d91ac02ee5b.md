# Output:

```
xi= 5
yi= 5
zi= 5
xf= 5.2
yf= 5.01
zf= 5.65
```

We can see that the results are different for parseInt and parseFloat. For xi and yi, we pass the string “5.2”. It is considered a string because it is within quotes. Even though there is a number within the quotes, we cannot use it in any mathematical operations without actually doing a parseInt or parseFloat. After completing a parseInt or parseFloat, it becomes a number. We also note that for all the values parseInt removes the decimal points and makes it a whole number. It does not round up or round down, just removes the decimal. ParseFloat retains the decimal value. So, if you want to work with decimals; use ParseFloat. If you want no decimal, then use ParseInt.

# Rounding numbers – Math.ceil(), Math.floor() and Math.round()

Next, let’s talk about rounding numbers. We use the functions **Math.Ceil(), Math.Floor() and Math.Round()**. Math.Ceil() rounds to the upper decimal value, Math.Floor() to the upper decimal value and Math.Round() to the nearest value (whether it’s upper or lower). Let’s look at a sample program.