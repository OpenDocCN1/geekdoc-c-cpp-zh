# Chapter 4: Location and Dimensions 85

The de.scrollHeight value is bigger when there is more web page below the bottom that can be scrolled to. In that case, there will be a scroll bar, harwidth is given the value of 17, which is the default width of scrollbars in all browsers. This value is subtracted from the full window width and the result is returned.

Otherwise, as is often the case if the browser is Internet Explorer, the code simply returns the value of whichever has a value, either de.clientWidth or document.body .clientWidth (allowing for either strict or quirks mode). This value already takes into account any scroll bar, so no code is required.

# How To Use It

To use this plug-in, simply call it and use the value returned, as in the following example, which passes the returned value to an alert () statement, where it is displayed:

```
<script>
window.onload = function() {
  alert('This browser has a window width of: ' + GetWindowWidth())
}
</script>
```

# The Plug-in

```
function GetWindowWidth() {
  var de = document.documentElement

if (BROWSER != 'IE') {
    var barwidth = de.scrollHeight > de.clientHeight ? 17 : 0
    return window.innerWidth - barwidth
  }

return de.clientWidth || document.body.clientWidth
}
```

# 26 GetWindowHeight()

This is the companion plug-in to GetWindowWidth(). It returns the height of the browser window, bearing in mind any scroll bars. In Figure 4-8 the usable area of this browser has been determined by this plug-in to be 124 pixels.

# About the Plug-in

This plug-in takes no arguments and returns the available height of the current window, taking any scroll bars into account.