# 282 Plug-In JavaScript: 100 Power Solutions

Here's an example that flies some list elements up from the browser bottom, with each arriving at its destination one second after the one it:

```
<b>How to become a millionaire:<ul>
  <li>span id='a'>Win the lottery</span></li>
  <li>span id='b'>Inherit the money</span></li>
  <li>span id='c'>Merry a millionaire</span></li>
  <li>span id='d'>Become a movie or pop star</span></li>
  <li>span id='e'>Invest $130/month in stocks for 40 years!</span></li>
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

Of inflation will eat away that amount, approximately each decade, the final amount in today's money would probably be closer to $250,000, pre tax and fees. Still, it's not bad for having invested $62,400 in total. By the way, I am not an investment advisor and this doesn't constitute advice for you to make any investments.

But I digress, so check the HTML part of the example. This HTML section creates a simple list and its element within spans. The <scripts> section then places the height of the browser into the variable h and five calls to FlyIn() with the different object IDs, a start location and animation periods from 1 to 5 seconds.

You can just fly the elements from the browser to top by specifying y=-20, or from the left or right edges using values of -W('object') -50 for the x argument when forming the line, or GetGetWidth() for the x argument if flying from the right. In fact, you can specify any x and y coordinates so like objects can fly in any direction.

**Tip** Because objects have to be a style position of 'absolute' in order to move about, if you have not enclosed the object (or a set of objects) in a suitable container with dimensions as a div or span, other elements of the HTML could move themselves to fill in the space previously occupied by the object (or objects). Tables are also good holders for objects that you will be flying in.