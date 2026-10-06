Therefore, if frw is less than padw or frh is less than padh, some padding must be applied. This is calculated by subtracting padw from frw and padh from frh. Along the way, padw and padh are passed through the Math.round() function to return integer values.

Then left and top are the new padding width and height to be given to the left and top of id. The variables right and bottom are also assigned these values, which means applying the padding width and height to the right and bottom of id. This is the code, which simply divides each padding value by two:

```
var left = Math.max(0, frw) - Math.round(padw) / 2
var right = left
var top = Math.max(0, frh) - Math.round(padh) / 2
var bottom = top
```

If the amount of padding to add to either the width or height of id is an odd number, then left and/ top (being half that number) will have a fractional part of .5.

For example, if 5 pixels padding is required, then left will have a value of 2.5, as right. This is because left contains the padding to add to one side, right contains the amount of padding to add to the top, and bottom contains the amount to add to the bottom of id.

However, most browsers don't allow floating point values for these properties (although, some do), left is compared with the value of Math.floor(left), which returns the value passed to it, less any fractional part. So if left has a value of 2.5, Math.floor(left) returns 2.

Therefore, if the following code does left have a fractional part, it removes it and gives that value plus one so that, in the current example, if left was 2.5 then it will have a value of 2, and right will be 3:

```
if (left != Math.floor(left)) {
  left = Math.floor(left)
  right = right + 1
}
```

The next five lines of code are the same, except they set top and bottom padding amounts, like this:

```
if (top != Math.floor(top)) {
  top = Math.floor(top)
  bottom = top + 1
}
```

The final statements actually set all the object's padding values, like this:

```
S(id).paddingLeft = Px(left)
S(id).paddingRight = Px(right)
S(id).paddingTop = Px(top)
S(id).paddingBottom = Px(bottom)
```