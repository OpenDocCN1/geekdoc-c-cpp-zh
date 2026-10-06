# 294 Plug-In JavaScript: 100 Power Solutions

The reason for requiring the two color arguments of coll and col2 is to allow for web pages of any color background, which can then be faded to any color of your choice for the light box frame. If your website has standard black text on a white background, I recommend you fading the light box between the color values #888888 (midgray) and #000000 (black). Or, you can be creative and fade between contrasts for an even more eye-catching effect. The argument will also greatly change the transition effect.

# The Plug-in

```
function Lightbox(id, coll, col2, opacity, msecs)
S(id).cursor = 'pointer';
if (0!('LB_DIV')) {
  var newdiv = document.createElement('div')
  newdiv.setAttribute('id', 'LB_DIV')
  document.body.appendChild(newdiv)
}
S(document.body).overflow = HID
Hide(Array(id, 'LB_DIV'))
Locate('LB_DIV', ABS, 0, 0)
Resize('LB_DIV', GetWindowWidth(), GetWindowHeight())
S('LB_DIV').zIndex = ZINDEX
Opacity(id, 0)
Position(id, ABS)
S(id).zIndex = ++ZINDEX
Show(Array(id, 'LB_DIV'))
Center(id)
Fade('LB_DIV', 0, opacity, msecs)
FadeIn(id, 'LB_DIV', coll, col2, 'back', msecs, 1)
O(id).onclick = DismissLB()
function DismissLB() {
Fade('LB_DIV', opacity, msecs)
ColorFade('LB_DIV', coll, col2, 'back', msecs, 1)
Chain(Array(
InsVars('FadeOut(Array('#1', 'LB_DIV'))', #2, "0", id, msecs),
InsVars('Hide(Array('#1', 'LB_DIV'))', id,
  "S(document.body, 'overflow', 'auto')")
))
))
```