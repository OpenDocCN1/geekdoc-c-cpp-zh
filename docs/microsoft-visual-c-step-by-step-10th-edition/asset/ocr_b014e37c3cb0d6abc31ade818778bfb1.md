```
if (seconds == 59)
{
  seconds = 0;
  minutes++;
}
```

Associate different statements with different values of a controlling expression

Use a switch statement. For example:

```
switch (current)
{
  case 0:
    ..
    break;
  case 1:
    ..
    break;
  default:
    ..
    break;
}
```

Assign a value to a variable based on different values of a controlling expression

Use a switch expression. For example:

Click here to view code image

```
string result = current switch
{
  < 0 => "below zero",
  0 => "zero",
  > 0 and < 100 => "between zero and a hundred",
  => "greater than a hundred"
}
```

![](bbox=[0.574, 0.763, 0.861, 0.773])