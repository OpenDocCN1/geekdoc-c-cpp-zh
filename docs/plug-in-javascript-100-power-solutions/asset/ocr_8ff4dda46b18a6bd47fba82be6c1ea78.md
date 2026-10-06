# 40 Plug-In JavaScript: 100 Power Solutions

```
else if (NavCheck('Chrome')) BROWSER = 'Chrome'
else if (NavCheck('iPod')) BROWSER = 'iPod'
else if (NavCheck('iPhone')) BROWSER = 'iPhone'
else if (NavCheck('iPad')) BROWSER = 'iPad'
else if (NavCheck('Android')) BROWSER = 'Android'
else if (NavCheck('Safari')) BROWSER = 'Safari'
else if (NavCheck('Gecko')) BROWSER = 'Firefox'
else BROWSER = 'UNKNOWN'
```

```
document.onmousemove = CaptureMouse
document.onkeydown = CaptureKeyboard
document.onkeypress = CaptureKeyboard

document.onmouseout = function() { MOUSE_IN = false }
document.onmouseover = function() { MOUSE_IN = true }
document.onmouseup = function() { MOUSE_DOWN = false }
document.onmousedup = function() { MOUSE_DOWN = true }
```

```
function NavCheck(check) {
  return navigator.userAgent.indexOf(check) != -1
}
```

# 4 CaptureMouse()

This plug-in is called only by the Initialize() function, and you should not to call it yourself. What it does is attach to the mouse movement event, updating various variables with details about the mouse position, as shown in Figure 3-4.

# About the Plug-in

This plug-in attaches to the .onmousemove event, updating the global variables MOUSE_X, MOUSE_Y, SCROLL_X, and SCROLL_Y. The event passes the value e to it, which is only used by browsers other than Internet Explorer. It does not require you to pass it any arguments, nor does it return any values.

> Figure 3-4
This plug-in lets you know where the mouse pointer is.

![](bbox=[0.305, 0.713, 0.843, 0.863])