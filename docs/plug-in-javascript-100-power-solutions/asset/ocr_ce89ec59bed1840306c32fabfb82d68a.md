# Chapter 8: Menus and Navigation 255

Next, four style properties are set to give the first div mouse pointer cursor, to give a little padding to the image, to provide a 1 pixel border between the header and the content, and to set the text to full justification. None of these things are necessary, but they are showed how you can add a little styling from JavaScript as easily as you can from a <style> section of HTML.

Finally, the onclick event of the div is set to call the BrowserWindow() plug-in.

Note Because I used a table as the container object for this pop-up, it does not handle the 'deflate' or 'zoom' transitions at all, since table dimensions are fixed and will not collapse on demand. If you wish to create a pop-up window that uses either of these transitions, you will need to build your container object using divs, spans, and CSS.

# The Plug-in

```
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