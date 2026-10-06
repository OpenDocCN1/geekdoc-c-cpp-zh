# Chapter 10: Audio and Visual Effects 309

Next, the type argument is tested to see if it has a value. If not, it is given the value
’‘pie’, which, therefore, becomes the default for no type is given:

```
if (typeof type == UNDEF) type = 'pie'
```

Then title is passed through the escape() function to make it suitable for passing in
a query URL tail, and title is then placed in the variable t1. Meanwhile, the
keyword for the chart type to send to Google is looked up by referencing the type
in the arguments array, as follows (that if, for example, type has the value
‘bar’, t2 will be assigned the value ‘bg’, and so on):

```
var t1 = escape(title)
var t2 = types[type]
```

After this, a selection of arguments are required for most charts such as the chart’s
title, width, height, and so on are assembled into the variable tail, each separated by
&amp; like this:

```
var tail = 'chtt='
 + t1
+ &amp;cht='
 + t2
+ &amp;chs='
 + width + 'x' + height
+ &amp;chb=' + bwidth
+ &amp;chxt=x,y'
+ &amp;chd=:' + data
```

If, then values for have been passed to the plug-in, a set of first if () statements
adds other arguments to tail:

```
if (tcolor && tsize) tail += '&amp;chts=' + tcolor + ',' + tsize
if (labels) tail += '&amp;ch-li=' + labels
if (legends) tail += '&amp;chdl=' + legends
if (colors) tail += '&amp;chco=' + colors
if (bgfill) tail += '&amp;chbg=s,' + bgfill
```

With now containing the completed query string, it is appended to the Google
Charts URL and then placed in an <img> ... tag, which is then assigned to the HTML of id:

```
Html(id, "<img src='http://chart.apis.google.com/chart? + +
tail + ' />")
```

This results in the chart displaying within the inner container.

# To Use It

To use this plug-in, start with an empty div, span, or other container that has an innerHTML
property, then pass this object along all the required parameters to the plug-in, and
in this example:

```
<div id='chart'></div>
<script>
window.onload = function() {
```