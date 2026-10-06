# Plug-In JavaScript: 100 Power Solutions

# How It Works

The plug-in uses a for() loop to assemble a final string created from num copies of str, and then returns the new string.

# How To Use It

To use this function, pass it a string and a number, like this:

```
string = 'Three cheers for the winner. ' +
StrRepeat('Hip, Hip Hooray', 3)
alert(string)
```

This code places the repeated cheer into string and displays it using a call to the JavaScript alert() function.

# The Plug-In

```
function StrRepeat(str, num)
{
  var tmp = ''
  for (var j = 0; j < num; ++j)
    tmp += str
  return tmp
}
```

# HexDec()

The final plug-ins in this chapter are to do with handling hexadecimal numbers, something you have to do quite often in JavaScript, particularly when managing colors. This one converts a hexadecimal number into decimal, as shown by Figure 3-17.

![](bbox=[0.125, 0.676, 0.834, 0.876])