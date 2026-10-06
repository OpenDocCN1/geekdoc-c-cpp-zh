
## Chapter 9: Text Effects

The variables tox and toy save the current location of the object as a record of where to fly into it. The start location for the animation is then placed in fromx and from, the step value for each dimension of frame is stored in xstep and ystep, and the counter is initialized.

Finally, in the setup section, the id is released from the HTML and given a style position property of 'absolute', using the global variable ABS. This allows it to be moved anywhere within the document. Next, the setInterval() function is called to start repeating interrupts by the DoFlyIn() subfunction every INTERVAL milliseconds. The result of calling the function is saved in iid to be used later when clearInterval() is called:

```
Position(id, ABS)
var iid = setInterval(DoFlyIn, INTERVAL)
```

## The DoFlyIn() Function

This function uses the GoTo() plug-in to move to each location in the animation, like this:

```
GoTo(id, fromx * xstep * count, fromy - ystep * count)
```

An if statement checks whether it has a value greater than or equal to msecs / INTERVAL. If it does, the fly-in has completed and the following code is executed, but whether it does or doesn't equal that value, count is incremented after the test is, like this:

```
if (count++ >= msecs / INTERVAL)
{}
```

If the fly-in has finished, the FI_Flag property of id is set to false to indicate this, GoTo() is placed at exactly the correct location (because xstep and ystep will use be floating points and the final values calculated using them could be off by a pixel or two). The repeating interrupts are stopped with a call to clearInterval(), like this:

```
O(id).FI_Flag = false
GoTo(id, tox, toy)
clearInterval(iid)
```

The function then returns, if the fly-in hasn't yet finished, it will be called again in INTERVAL milliseconds, and so on until the animation is completed.

## How To Use It

To use this plug-in, pass an object and specify where you want the object to fly in from by providing relative horizontal and vertical coordinates in the next two arguments. You also have to tell the plug-in how long the animation should take in milliseconds.

## 282 Plug-In JavaScript: 100 Power Solutions

Here's an example that flies some list elements up from the browser bottom, with each arriving at its destination one second after the one it:

```
<b>How to become a millionaire:</b><ul>
  <li><span id='a'>Win the lottery</span></li>
  <li><span id='b'>Inherit the money</span></li>
  <li><span id='c'>Merry a millionaire</span></li>
  <li><span id='d'>Become a movie or pop star</span></li>
  <li><span id='e'>Invest $130/month in stocks for 40 years!</span></li>
</ul></body>
```

```
<script>
window.onload = function () {
  h = GetWindowHeight()

  FlyIn('a', 0, 1000)
  FlyIn('b', 0, 2000)
  FlyIn('c', 0, 3000)
  FlyIn('d', 0, 4000)
  FlyIn('e', 0, 5000)
}
</script>
```

In case you were wondering, statistically the stock market has returned 11 percent on average per year over the last few decades. And, according to any compound interest calculator, $130 invested every over 40 years, and at an average of 11% per year, will return a gross amount of $1,007,490.02, after taxes and fees.

Inflation will eat away that amount, approximately each decade, the final amount in today's money would probably be closer to $250,000, pre tax and fees. Still, it's not bad for having invested $62,400 in total. By the way, I am not an investment advisor and this doesn't constitute advice for you to make any investments.

But I digress, so check the HTML part of the example. This HTML section creates a simple list and its element within spans. The <script> section then places the height of the browser into the variable h and five calls to FlyIn() with the different object IDs, a start location and animation periods from 1 to 5 seconds.

You can just fly the elements from the browser to top by specifying y=-20, or from the left or right edges using values of -W('object') -50 for the x argument when forming the line, or GetWidth() for the x argument if flying from the right. In fact, you can specify any x and y coordinates so like objects can fly in any direction.

**Tip** Because objects have to be a style position of 'absolute' in order to move about, if you have not enclosed the object (or a set of objects) in a suitable container with dimensions as a div or span, other elements of the HTML could move themselves to fill in the space previously occupied by the object (or objects). Tables are also good holders for objects that you will be flying in.

## Chapter 9: Text Effects 283

## The Plug-in

```javascript
function FlyIn(id, x, y, msecs)
{
  if (id instanceof Array)
  {
    for (var j = 0; j < id.length; ++j)
      FlyIn(id[j], x, y, msecs)
    return
  }

  if (O(id).FI_Flag) return
  else O(id).FI_Flag = true

  var tox = Get(id)
  var toy = Get(id)
  var fromx = x
  var fromy = y
  var xstep = msecs / INTERVAL
  var ystep = msecs / INTERVAL
  var count = 0

  Position(id, ABS)
  var iid = setInterval(DoFlyIn, INTERVAL)
}

function DoFlyIn()
{
  GoTo(id, fromx * xstep * count, fromy - ystep * count)

  if (count++ >= msecs / INTERVAL)
  {
    O(id).FI_Flag = false
    GoTo(id, tox, toy)
    clearInterval(iid)
  }
}
```
