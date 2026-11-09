# Breaking down the code:

```
```javascript
var num1=parseFloat(document.getElementById("num1").value);
var num2=parseFloat(document.getElementById("num2").value);
```
```

These lines store the values of the two numbers filled in by the user in two variables num1 and num2.

```
```javascript
if ((num1+num2)<15)
```
```

This checks if the sum of both numbers is greater than 15.

```
```javascript
{
document.write('Sum of two numbers is less than 15');
}
```
```

The above loop activates if the sum is less than 15 and prints out ‘Sum of two numbers is less than 15.’

```
```javascript
else
{
document.write('Sum of two numbers is greater than or equal to 15');
}
```
```

The above loop activates if the sum is greater than 15 and prints out ‘Sum of two numbers is greater than or equal to 15.’