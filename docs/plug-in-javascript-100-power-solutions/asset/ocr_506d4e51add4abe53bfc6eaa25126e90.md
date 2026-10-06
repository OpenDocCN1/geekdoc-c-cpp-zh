# Chapter 3: The Core Plug-ins 35

```
tmp.push(S(id[j], property, value)
return tmp
```

```
if (typeof property != UNDEF && typeof value != UNDEF)
{
  try { return O(id).style[property] = value }
  catch (e) { alert('PJ - Unknown ID: ' + id) }
}\else if (typeof id == 'object') return id.style
{
  try { return O(id).style }
  catch (e) { alert('PJ - Unknown ID: ' + id) }
}
```

# Initialize()

In order to set up the plug-ins use, you will have to call a small initialization plug-in at the start of your web pages. Previously mentioned, I recommend you always include the following two lines of code at the start of each:

```
<script src="PJ.js"></script>
<script>Initialize()</script>
```

Or if you are using the compressed version of the plug-ins, Pjssmall.js, you would use that file in place of Pjs.

This plug-in is the Initialize() function that is called by that code, and it prepares a wide range of functionality you can draw on, as shown in Figure 3-3, in the browser type is detected.

# About the Plug-in

This plug-in requires no arguments and does not return any. However, please refer to the table of variables, arrays, and functions in the next section, as very important global variables are set up by it.

Figure 3-3
Displaying the variable BROWSER after calling this plugin

![](bbox=[0.31, 0.73, 0.846, 0.915])