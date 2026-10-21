```
Switch (m)
{
    case 1:
        x = y;
        goto case 2;
    case 2:
        x = y + m
        goto default;
    default:
        x = y - m;
        break;
}
```

The goto mechanism enables us to jump backward and forward between cases and therefore arrange labels arbitrarily. Example:

```
Switch (m)
{
    default:
        x = y-m;
        break;
    case 2:
        x = y + m;
        goto default;
    case 1:
        x = y;
        goto case 2;
}
```

is perfectly valid.

Program 6.7 uses switch case to allow users to select the size of a cola can. Based on the user selection, the program prints the amount the user must pay for the particular type of can selected.

# Program 6.7 | ANOTHER SWITCH EXAMPLE

```
using System;
class SwitchExample
{
public static void Main()
{
Console.WriteLine("Select your Cola Can:");
Console.WriteLine("S=SMALL M=MEDIUM L=LARGE");
Console.Write("Please enter your option: ");
String s = Console.ReadLine();
int cost = 0;
switch(s)
{
case "S":
    cost += 10;
    break;
case "M":
    cost += 15;
```