
## 254 Plug-In JavaScript: Power Solutions

JavaScript is the free language built into all modern browsers and is the power behind dynamic HTML and the Ajax used for Web 2.0 websites. Plug-in JavaScript is aimed at people who have learned basic HTML (and perhaps a little CSS) but are interested in doing more. For more details please <a href='http://pluginjavascript.com' target='New'>visit the website</a>.

```html
</td>
</tr>
</table>

<script>
window.onload = function() {
  Hide('window')
  x = (GetWindowWidth() - 330) / 2
  y = (GetWindowHeight() - 245) / 2

  S('window').border = 'solid 2px'
  Position('window', ABS)
  PopDown('window', 'fade', null, null, 1, false)
  Resize('window', 330, 245)

  S('click').cursor = 'pointer'
  S('image').paddingRight = Px(10)
  S('content').border = 'solid 1px'
  S('content').textAlign = 'justify'

O('click').onclick = function() {
  BrowserWindow('window', 'header', 'close', x, y, true,
  'fade', null, null, 500, false)
}
</script>
```

The HTML section starts by creating a div that you can click to raise the pop-up. Underneath this is a table with three sections: a header, a button, and a center section. The <script> section of code starts by calculating the correct coordinates to place the pop-up in the center of the browser, gives the pop-up a solid border of 2 pixels, and uses the Position() plugin-in to get the pop-up style position of 'absolute', which releases from place to be moved anywhere within the document. You can use a style position of 'fixed' if you prefer to limit the pop-up to staying only within the browser's viewport into the document.

The PopDown() function is called with a value of 1 millisecond to quickly hide the pop-up away. It's important to use the transition type of 'fade' to later pop the window up because the transition types must match or you will get strange errors.

The window is then resized to ensure that it is of set dimensions and to prevent content overflowing from the pop-up, its overflow style property is set to 'hidden'.

![](img/95e4c43b430487125c342550cc090977_271_0.png)

## Chapter 8: Menus and Navigation 255

Next, four style properties are set to give the first div mouse pointer cursor, to give a little padding to the image, to provide a 1 pixel border between the header and the content, and to set the text to full justification. None of these things are necessary, but they are showed how you can add a little styling from JavaScript as easily as you can from a <style> section of HTML.

Finally, the onclick event of the div is set to call the BrowserWindow() plug-in.

Note: Because I used a table as the container object for this pop-up, it does not handle the 'deflate' or 'zoom' transitions at all, since table dimensions are fixed and will not collapse on demand. If you wish to create a pop-up window that uses either of these transitions, you will need to build your container object using divs, spans, and CSS.

## The Plug-in

```javascript
function BrowserWindow(id, headerid, closeid, x, y, bounds,
  type, w, h, msecs, interruptible)
{
Goto(id, x, y)
Popup(id, type, w, h, msecs, interruptible)
var browser = GetWidth()
var browser = getHeight()
var border = NoPx(S(id).borderLeftWidth) +
  NoPx(S(id).borderRightWidth)
var borderh = NoPx(S(id).borderTopWidth) +
  NoPx(S(id).borderBottomWidth)
var popup = W(id)
var popup = H(id)
S(closeid).cursor = 'pointer'
(id).onclick = BWTOFront
O(closeid).onclick = BWCloseWindow
O(headerid).onmousemove = BMove
PreventAction(headerid, 'select', true)
PreventAction(closeid, 'select', true)
function BWTOFront()
{
S(id).zIndex = ++ZINDEX
}
function BWCloseWindow()
{
Popup(id, type, w, h, msecs, interruptible)
}
function BMove()
{
BWTOFront()
S(headerid).cursor = 'move'
```

## 256 Plug-In JavaScript: 100 Power Solutions

```javascript
var xoffset = MOUSE_X - X(id)
var yoffset = MOUSE_Y - Y(id)
var iid     = setInterval(DoBWMove, 10)
```

```javascript
function DoBWMove() {
  var x = MOUSE_X - xoffset
  var y = MOUSE_Y - yoffset

  if (bounds) {
    var r = browser - popupw - borderw + SCROLL_X
    var b = browserh - popup - border + SCROLL_Y
    x = Math.max(0, Math.min(x, r))
    y = Math.max(0, Math.min(y, b))
  }
}
```

```javascript
if (MOUSE_X < 0 || MOUSE_X > (browser + SCROLL_X) ||
    MOUSE_Y < 0 || MOUSE_Y > (browserh + SCROLL_Y) ||
    !MOUSE_DOWN || !MOUSE_IN) {
    clearInterval(iid)
    S(headerid).cursor = 'default'
  }

  Goto(id, x, y)
}
```

## CHAPTER 9

### Text Effects

## Plug-In JavaScript: 100 Power Solutions

This chapter provides you with a wide range of plug-ins offering text manipulation features. For example, you can enable text scrolling, either to the left or right, and you can choose how many times the scroll should repeat and disappear, as.

There are also typewriter and "matrix" effects to make text appear and disappear, as well as fading text, flying text into position, and even fancy ripple effects for drawing attention to important text.

## TextScroll()

With this plug-in, you can scroll selected text either left or right at a speed of your choosing and for a set number of times. Figure 9-1 shows two phrases. The top one is scrolling over the course of three seconds, and the bottom is scrolling over a period of one second.

## About the Plug-in

This plug-in takes an object that contains text and then scrolls it. It requires the following arguments:

- *id* An object, object ID, or array of objects and/or object IDs
- *dir* The direction of scrolling, 'left' or 'right'
- *number* The number of times to repeat the scroll, with 0 indicating infinite repeat
- *msecs* The number of milliseconds a full scroll should take

## Variables, Arrays, and Functions

| j | Description |
| :--- | :--- |
| j | Local variable for iterating through id if it is an array |
| copy | Local copy of the HTML contents if |
| len | Local variable containing the length of copy |
| freq | Local variable containing the period in milliseconds between each call to DoTextScroll() |
| ctrl1, ctrl2 | Local counters for counting the characters in a string |
| iid | Local variable returned from setInterval(), to be used when clearInterval() |
| innerText | Property of id in non-Firefox browsers containing the text |
| textContent | Property of id in Firefox browsers containing the text |
| TS_Flag | Property of id that is true when a scroll is in progress |
| LT | Global variable with the value 'left' |
| Math.round() | Function to turn a floating point number into an integer |
| substr() | Function to return a substring |
| setInterval() | Function start repeating interrupts |
| clearInterval() | Function to stop repeating interrupts |
| DoTextScroll() | Subfunction to perform the scrolling |
| Html() | Plug-in to return the HTML content of an object |

## Chapter 9: Text Effects 259

![](img/95e4c43b430487125c342550cc090977_276_0.png)

Figure 9-1: Scrolling text is easy with this plug-in.

## How It Works

This plug-in begins by iterating through id if it is an array, recursively calling itself to individually deal with each element, like this:

```javascript
if (id instanceof Array)
{
  for (var j = 0; j < id.length; ++j)
    TextScroll(id[j], dir, number, msecs)
  return
}
```

The TS_Flag property of id is tested. If it's true, a scroll is already operating on the object so the function returns. Otherwise, the property is set to true to indicate that the scroll is in action on the id, as follows:

```javascript
if (O(id).TS_Flag) return
else O(id).TS_Flag = true
```

Next, local variables are set up to hold the content of id, the length of the text, the frequency at which DoTextScroll() function must be called in order to scroll msecs milliseconds, a couple of counters and, finally, the repeating interrupts are set up with a call to setInterval(), with these statements:

```javascript
var copy = Html(id)
var len = copy.length
var freq = Math.round(msecs) / len
var ctr = 0
var id = setInterval(DoTextScroll, freq)
```

### The DoTextScroll Subfunction

This function is called repeatedly at a frequency that will ensure a full scroll of the text will take msecs milliseconds. It determines whether to scroll left or right by checking the dir argument and then modifying the string accordingly. If scrolling left, characters are
