# 196 Plug-In JavaScript: 100 Power Solutions

Finally, within the chain of commands the previous zoom instructions have been replaced with calls to FadeIn(), WaitKey(), and FadeOut().
If you press any key except the space bar when the message is displayed, the ship will proceed on its way and continuing in a loop. However, if the key press the space bar, then the expression at the start of the While() command will evaluate to true, and the chain will stop repeating.

# The Plug-in

```
function WaitKey() {
  GetLastKey()
  setTimeout(DoWaitKey, INTERVAL)
}

function DoWaitKey() {
  if (KEY_PRESS == '') NextInChain()
  else setTimeout(DoWaitKey, INTERVAL)
}
```

# Flip()

This plug-in provides a professional flip effect that will appear to spin an object around to reveal its reverse. Three different spin effects are provided, making this a great way to provide interesting visual effects and even more information on your web pages.

In Figure 7-6, the photograph of Albert Einstein is attached to a mouse event so that the mouse passes over the image, it flips to reveal more information. It is not possible to show you the effect in the medium of a book, but think of the image as a trading or similar type of card with a picture on the front and further information on the back. Figure 7-7 shows the "reverse" of image as the mouse is held over.

Figure 7-6
The image in this web page is reversible when moused over.

![](bbox=[0.305, 0.637, 0.837, 0.932])